---
icon: lock
---

# Webhooks

App Access Tokens and User Access Tokens can access this.

## Headers

| Header                         | Type                 | Short Description                      |
| ------------------------------ | -------------------- | -------------------------------------- |
| `Kick-Event-Message-Id`        | ULID                 | Unique message ID, idempotent key      |
| `Kick-Event-Subscription-Id`   | ULID                 | Subscription ID associated with event  |
| `Kick-Event-Signature`         | Base64 Encode String | Signature to verify the sender         |
| `Kick-Event-Message-Timestamp` | RFC3339 Date-time    | Timestamp of when the message was sent |
| `Kick-Event-Type`              | string               | e.g. `chat.message.sent`               |
| `Kick-Event-Version`           | string               | e.g. `1`                               |

## Webhook Sender Validation

`Kick-Event-Signature` header is used to validate if a request has come from the Kick servers. This is to prevent anyone who finds an app's webhook endpoint from sending fake events.

### Kick Public Key

Any request that is sent from our servers will have a signature signed by our Private Key, which can be verified using the Public Key.

Fetch the public key from the hosted endpoint. Do not hardcode it. The key can be rotated at any time, and a hardcoded copy will fail verification after a rotation.

```
https://api.kick.com/public/v1/public-key
```

[Public Key](../apis/public-key.md)

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
	"io"
	"net/http"
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

// Fetch the current public key. Do not hardcode it: Kick may rotate it at any time.
resp, err := http.Get("https://api.kick.com/public/v1/public-key")
if err != nil {
    return err
}
defer resp.Body.Close()

pemBytes, err := io.ReadAll(resp.Body)
if err != nil {
    return err
}

pubkey, err := ParsePublicKey(pemBytes)

// Create the Signature to compare
signature := []byte(fmt.Sprintf("%s.%s.%s", messageID, timestamp, body))

// Verify the Header
err := Verify(pubkey, signature, headers["Kick-Event-Signature"])

```

## Disabling of Webhooks

If an app's webhook continually fails to process an event for over a day, Kick automatically unsubscribes the app from that event.

The app will then need to resubscribe to that particular event.
