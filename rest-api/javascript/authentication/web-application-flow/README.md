# Authorization code flow

This sample project demonstrates how a registered app can request authorization from Uphold users to perform actions on their behalf,
by using the [authorization code OAuth flow](https://oauth.net/2/grant-types/authorization-code/).
For further background, please refer to the [API documentation](https://uphold.com/en/developer/api/documentation).

## Summary

This flow is **recommended for web applications** that wish to retrieve information about a user's Uphold account,
or take actions on their behalf.

This process, sometimes called "3-legged OAuth", requires three steps, each initiated by one of the three actors:

1. The **user** navigates to Uphold's website, following an authorization URL generated by the app,
   where they log in and authorize the app to access their Uphold account;
2. **Uphold** redirects the user back to the app's website, including a short-lived authorization code in the URL;
3. The **application**'s server submits this code to Uphold's API, obtaining a long-lived access token in response.
   (Since this final step occurs in server-to-server communication, the actual code is never exposed to the browser.)

This example sets up a local server that can be used to perform the OAuth web application flow cycle as described above.

## Requirements

To run this example, you must have:

- Node.js v13.14.0 or later
- An account at <https://sandbox.uphold.com>

## Setup

- Run `npm install` (or `yarn install`)
- [Create an app on Uphold Sandbox](https://sandbox.uphold.com/dashboard/profile/applications/developer/new)
  with the redirect URI field set to `https://localhost:3000/callback`
  (you may use a different port number, if you prefer).
  Note that this demo expects at least the `user:read` scope to be activated.
- Create a `.env` file based on the `.env.example` file, and populate it with the required data.
  Make sure to also update the `SERVER_PORT` if you changed it in the previous step.

## Run

- Run `node index.js`
- Open the URL printed in the command line.
  - **Attention:** Since the certificate used in this demo is self-signed, not all browsers will allow navigating to the page.
    You can use Firefox or Safari, which will display a warning but allow you to proceed regardless.
    Alternatively, you can navigate to `chrome://flags/#allow-insecure-localhost` in Chromium-based browsers,
    to toggle support for self-signed localhost certificates.
- Click the link in the page to navigate to Uphold's servers.
- Accept the application's permission request.

Once the authorization is complete and an access token is obtained,
the local server will use it to make a test request to the Uphold API.
The output will be printed in the command line.