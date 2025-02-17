---
icon: lock
---

# Webhooks

App Access Tokens and User Access Tokens can access this.

## Headers

| Header                         | Type                 | Short Description                      |
|--------------------------------|----------------------|----------------------------------------|
| `Kick-Event-Message-Id`        | ULID                 | Unique message ID, idempotent key      |
| `Kick-Event-Signature`         | Base64 Encode String | Signature to verify the sender         |
| `Kick-Event-Message-Timestamp` | RFC3339 Date-time    | Timestamp of when the message was sent |
| `Kick-Event-Type`              | string               | e.g. `channel:write`                   |
| `Kick-Event-Version`           | string               | e.g. `1`                               |

## Webhook Sender Validation

`Kick-Event-Signature` header is used to validate if a request has come from the Kick servers. This is to prevent anyone who finds an app's webhook endpoint from sending fake events.

### Kick Public Key

This is the Kick public key. Any request that is sent from our servers will have a signature signed by our Private Key, which can be decrypted using this Public Key.

```
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAq/+l1WnlRrGSolDMA+A8
6rAhMbQGmQ2SapVcGM3zq8ANXjnhDWocMqfWcTd95btDydITa10kDvHzw9WQOqp2
MZI7ZyrfzJuz5nhTPCiJwTwnEtWft7nV14BYRDHvlfqPUaZ+1KR4OCaO/wWIk/rQ
L/TjY0M70gse8rlBkbo2a8rKhu69RQTRsoaf4DVhDPEeSeI5jVrRDGAMGL3cGuyY
6CLKGdjVEM78g3JfYOvDU/RvfqD7L89TZ3iN94jrmWdGz34JNlEI5hqK8dd7C5EF
BEbZ5jgB8s8ReQV8H+MkuffjdAj3ajDDX3DOJMIut1lBrUVD1AaSrGCKHooWoL2e
twIDAQAB
-----END PUBLIC KEY-----
```

### Signature Creation

The signature is created through the concatenation of the following values into a single string, separated by a `.`:

* `Kick-Event-Message-Id`
* `Kick-Event-Message-Timestamp`
* The raw body of the request

```go
signature := []byte(fmt.Sprintf("%s.%s.%s", messageID, timestamp, body))
```

Once concatenated, the body will be signed with the Kick Private Key.

### Examples

Here are some examples of verifying the signature in different languages:

#### Golang

```go
import (
	"crypto/rsa"
	"crypto/x509"
	"encoding/pem"
	"errors"
)

func ParsePublicKey(bs []byte) (rsa.PublicKey, error) {
	block, _ := pem.Decode(bs)
	if block == nil {
		return rsa.PublicKey{}, errors.New("not decodable key")
	}

	if block.Type != "PUBLIC KEY" {
		return rsa.PublicKey{}, errors.New("not public key")
	}

	parsed, err := x509.ParsePKIXPublicKey(block.Bytes)
	if err != nil {
		return rsa.PublicKey{}, err
	}

	publicKey, ok := parsed.(*rsa.PublicKey)
	if !ok {
		return rsa.PublicKey{}, errors.New("not expected public key interface")
	}

	return *publicKey, nil
}


import (
	"crypto"
	"crypto/rsa"
	"crypto/sha256"
	"encoding/base64"
)

func Verify(publicKey *rsa.PublicKey, body []byte, signature []byte) error {
   decoded := make([]byte, base64.StdEncoding.DecodedLen(len(signature)))

   n, err := base64.StdEncoding.Decode(decoded, signature)
   if err != nil {
       return err
   }


   signature = decoded[:n]
   hashed := sha256.Sum256(body)


   return rsa.VerifyPKCS1v15(publicKey, crypto.SHA256, hashed[:], signature)
}

// Parse the Public Key
pubkey, err := keysx.ParsePublicKey([]byte(`
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAq/+l1WnlRrGSolDMA+A8
6rAhMbQGmQ2SapVcGM3zq8ANXjnhDWocMqfWcTd95btDydITa10kDvHzw9WQOqp2
MZI7ZyrfzJuz5nhTPCiJwTwnEtWft7nV14BYRDHvlfqPUaZ+1KR4OCaO/wWIk/rQ
L/TjY0M70gse8rlBkbo2a8rKhu69RQTRsoaf4DVhDPEeSeI5jVrRDGAMGL3cGuyY
6CLKGdjVEM78g3JfYOvDU/RvfqD7L89TZ3iN94jrmWdGz34JNlEI5hqK8dd7C5EF
BEbZ5jgB8s8ReQV8H+MkuffjdAj3ajDDX3DOJMIut1lBrUVD1AaSrGCKHooWoL2e
twIDAQAB
-----END PUBLIC KEY-----
`))

// Create the Signature to compare
signature := []byte(fmt.Sprintf("%s.%s.%s", messageID, timestamp, body))

// Verify the Header
err := Verify(pubkey, signature, headers["Kick-Event-Signature"])

```

## Retrying Sending of Events

Kick will attempt to send a webhook 3 times over a period of time until a 200 response is made by the server.

## Disabling of Webhooks

After a certain threshold of errors are received from an app's webhook endpoint, Kick may automatically unsubscribe the app from receiving webhooks.

The app will then need to resubscribe to webhooks.
