---
icon: bolt
description: Build your first Kick API integration
---

# Node.js Quickstart Guide

This guide walks you through creating a simple Node.js application that authenticates users with Kick OAuth and makes API calls. Perfect for beginners getting started with the Kick Public API.

## What You'll Build

By the end of this guide, you'll have a working Node.js app that:
- Authenticates users with Kick OAuth 2.1
- Securely handles access tokens
- Makes authenticated API calls to fetch user data

## Prerequisites

Before you begin, make sure you have:

- **Node.js 16+** installed ([download here](https://nodejs.org/))
- **A Kick account** with 2FA enabled ([sign up here](https://kick.com))
- **ngrok** for local development ([download here](https://ngrok.com/download))
- **Basic JavaScript knowledge** (variables, functions, async/await)

{% hint style="info" %}
**Why ngrok?** OAuth requires a publicly accessible URL. ngrok creates a secure tunnel to your local development server, making it accessible from the internet.
{% endhint %}

## Step 1: Set Up Your Development Environment

### 1.1 Clone the Repository

Open your terminal and clone the Kick API examples repository:

```bash
git clone https://github.com/KickEngineering/kick-public-api-examples.git
cd kick-public-api-examples/oauth-nodejs-quickstart
```

### 1.2 Install Dependencies

Install the required Node.js packages:

```bash
npm install
```

**What these packages do:**
- `express` - Web framework for building the server
- `express-session` - Manages user sessions (stores OAuth state)
- `axios` - HTTP client for making API requests

The project is already configured with ES modules and includes a complete `app.js` file with all the OAuth implementation.

## Step 2: Create Your Kick OAuth Application

### 2.1 Enable Two-Factor Authentication (2FA)

1. Go to your [Kick Account Settings > Security](https://kick.com/settings/security)
2. Enable **Two-Factor Authentication** (required for developer access)

### 2.2 Start ngrok

Before creating your OAuth app, start ngrok in your terminal to get your public URL:

```bash
ngrok http 3000
```

You'll see output like this:

```text
Forwarding  https://abc123.ngrok-free.dev -> http://localhost:3000
```

**Copy your ngrok URL** (e.g., `https://abc123.ngrok-free.dev`) - you'll need it in the next step.

{% hint style="warning" %}
**Important:** Keep ngrok running! If you close it, you'll get a new URL and need to update your OAuth app settings.
{% endhint %}

### 2.3 Create Your OAuth Application

1. Go to [Kick Developer Settings](https://kick.com/settings/developer)
2. Click **"Create Application"**
3. Fill in the details:
   - **Application Name:** "My First Kick App" (or any name you prefer)
   - **Redirect URI:** `https://YOUR_NGROK_URL/callback` (e.g., `https://abc123.ngrok-free.dev/callback`)
   - **Scopes:** Select `user:read` (allows reading user profile data)
4. Click **"Create"**
5. **Copy your Client ID and Client Secret** - you'll need these in the next step

{% hint style="danger" %}
**Security Note:** Treat your Client Secret like a password. Never commit it to version control or share it publicly.
{% endhint %}

## Step 3: Configure Your Application

### 3.1 Configure Your Credentials

Open `app.js` in your code editor and replace these three values (around lines 164-166):

```javascript
const CLIENT_ID = "your_client_id_here";           // From Step 2.3
const CLIENT_SECRET = "your_client_secret_here";   // From Step 2.3
const REDIRECT_URI = "https://abc123.ngrok-free.dev/callback"; // Your ngrok URL + /callback
```

## Step 4: Run Your Application

### 4.1 Start the Server

```bash
npm start
```

You should see:

```text
Server running on http://localhost:3000
Public URL: Check your ngrok terminal for the URL
```

### 4.2 Test Your Application

1. Open your **ngrok URL** in your browser (e.g., `https://abc123.ngrok-free.dev`)
2. Click **"Login with Kick"**
3. You'll be redirected to Kick's authorization page
4. Click **"Authorize"** to grant permissions
5. You'll be redirected back to your app and see your user data!

{% hint style="success" %}
**Congratulations!** You've successfully built your first Kick API integration.
{% endhint %}

## Making API Calls

Once you have an access token, making API calls is simple:

```javascript
const apiResp = await axios.get(`${KICK_API}/users`, {
  headers: { Authorization: `Bearer ${access_token}` },
});
```

The access token is sent in the `Authorization` header as a Bearer token.

## Next Steps

Now that you have a working integration, here are some ideas to expand your app:

### 1. Explore More API Endpoints

Try calling different Kick API endpoints:

```javascript
// Get channel information
const channel = await axios.get(`${KICK_API}/channels/username`, {
  headers: { Authorization: `Bearer ${access_token}` },
});

// Get livestream data
const livestream = await axios.get(`${KICK_API}/channels/username/livestream`, {
  headers: { Authorization: `Bearer ${access_token}` },
});
```

See the [Users API](../apis/users.md) and other API documentation for all available endpoints.

### 2. Request Additional Scopes

Need more permissions? Update the `SCOPES` variable:

```javascript
const SCOPES = "user:read channel:read chat:read"; // Multiple scopes
```

Available scopes:
- `user:read` - Read user profile data
- `channel:read` - Read channel information
- `chat:read` - Read chat messages
- `chat:write` - Send chat messages
- And more - see [Scopes](../scopes/scopes.md)

### 3. Implement Token Refresh

Access tokens expire. Implement refresh token logic to keep users authenticated:

```javascript
async function refreshAccessToken(refresh_token) {
  const form = new URLSearchParams({
    grant_type: "refresh_token",
    client_id: CLIENT_ID,
    client_secret: CLIENT_SECRET,
    refresh_token: refresh_token,
  });

  const response = await axios.post(`${KICK_AUTH}/oauth/token`, form, {
    headers: { "Content-Type": "application/x-www-form-urlencoded" },
  });

  return response.data;
}
```

### 4. Add Environment Variables

For production, use environment variables instead of hardcoding secrets:

```bash
npm install dotenv
```

Create a `.env` file:

```
CLIENT_ID=your_client_id
CLIENT_SECRET=your_client_secret
REDIRECT_URI=https://your-domain.com/callback
SESSION_SECRET=your_random_session_secret
```

Update your code:

```javascript
import dotenv from 'dotenv';
dotenv.config();

const CLIENT_ID = process.env.CLIENT_ID;
const CLIENT_SECRET = process.env.CLIENT_SECRET;
// ... etc
```

### 5. Build a Real Application

Ideas for what to build:
- **Chat bot** - Automate chat interactions
- **Stream dashboard** - Display live stream statistics
- **Moderation tools** - Build custom moderation interfaces
- **Analytics** - Track channel growth and engagement
- **Alerts** - Send notifications for stream events

## Troubleshooting

### "State mismatch or missing code"

**Cause:** The state parameter doesn't match, or the authorization code is missing.

**Solutions:**
- Make sure cookies are enabled in your browser
- Check that your session secret is set correctly
- Try clearing your browser cookies and restarting

### "Token exchange failed"

**Cause:** The authorization code couldn't be exchanged for an access token.

**Solutions:**
- Verify your `CLIENT_ID` and `CLIENT_SECRET` are correct
- Ensure your `REDIRECT_URI` exactly matches what's in your Kick app settings
- Check that your ngrok tunnel is still running
- Look at the console error message for specific details

### "API call failed"

**Cause:** The API request failed (invalid token, network error, etc.)

**Solutions:**
- Check that your access token is valid
- Verify you have the correct scopes for the endpoint you're calling
- Look at the console error message for specific details

### ngrok URL Changed

**Cause:** Each time you restart ngrok, you get a new URL.

**Solutions:**
- Update the `REDIRECT_URI` in your `app.js`
- Update the Redirect URI in your [Kick app settings](https://kick.com/dashboard/settings/applications)
- Consider getting a [free ngrok account](https://ngrok.com/pricing) for a persistent URL

### "Cannot GET /callback"

**Cause:** The callback route isn't working.

**Solutions:**
- Make sure your server is running (`npm start`)
- Verify the route is defined in your `app.js`
- Check that you're using the correct ngrok URL

## Need Help?

If you're stuck or have questions:

1. Check the [Troubleshooting](#troubleshooting) section above
2. Review the [OAuth 2.1](generating-tokens-oauth2-flow.md) documentation
3. Explore the [APIs](../apis/users.md) documentation
4. Check the [Contributing Guide](../CONTRIBUTING.md)

## What's Next?

You've completed the Node.js Quickstart! Here are some next steps:

1. **Explore the API** - Try different endpoints and scopes
2. **Build something cool** - Create a chat bot, dashboard, or tool
3. **Share your project** - Show the community what you built
4. **Contribute** - Help improve the documentation

Happy coding!
