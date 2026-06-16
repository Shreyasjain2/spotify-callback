<div align="center">
  <img src="https://storage.googleapis.com/pr-newsroom-wp/1/2018/11/Spotify_Logo_RGB_Green.png" alt="Spotify Logo" width="300" />
</div>

<div align="center">
  <h3><a href="https://shreyasjain2.github.io/Portfolio/" target="_blank">Click here to view the live portfolio and test the player</a></h3>
</div>

# Spotify Mini Player Integration

A seamless, integrated mini Spotify Web Player designed to inject directly into your web environment. This repository contains the frontend integration as well as the Tampermonkey script required to securely manage playback and authentication without compromising page aesthetics.

## Overview

This project consists of two main components:
1. **The Web Interface**: A custom frontend (such as a portfolio website) that handles user interaction and hidden triggers (like the Konami code).
2. **The Tampermonkey Userscript**: A secure, isolated script that bridges the Spotify Web Playback SDK with your browser, handling PKCE OAuth authentication, token management, and direct player controls.

## Prerequisites

To run the mini player successfully, you will need:
- A modern desktop web browser (Chrome, Edge, Firefox).
- A Spotify Premium account (required by the Spotify Web Playback SDK).
- The [Tampermonkey](https://www.tampermonkey.net/) browser extension installed.

## Setup Instructions

### 1. Install the Userscript

The core player logic is contained within the userscript. You must install this into Tampermonkey.

1. Open the Tampermonkey dashboard in your browser.
2. Click the **+** icon to create a new script.
3. Copy the contents of the userscript from this repository and paste it into the editor, completely replacing the default template.
4. Save the script.

### 2. Configure Spotify Developer Credentials

For authentication to work, you must provide your own Spotify API credentials. 

1. Navigate to the [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/).
2. Log in and click **Create App**.
3. Fill in the App Name and App Description.
4. In the **Redirect URIs** field, you must enter your exact callback URL for your local environment. 
   - *Example: `http://localhost:8080/spotify-callback/`*
5. Save the application and take note of your **Client ID**.
6. Open your installed Tampermonkey script and update the following configuration variables near the top of the file:

```javascript
const CLIENT_ID    = 'YOUR_SPOTIFY_CLIENT_ID_HERE';
const REDIRECT_URI = 'YOUR_REDIRECT_URI_HERE';
```

### 3. Triggering the Player

The userscript is configured to securely match and run on a specific domain.

To test the integration:
1. Navigate to the live site: [Click here to launch the portfolio](https://shreyasjain2.github.io/Portfolio/)
2. Once the page has loaded, you have two methods to summon the player:
   - **Keyboard Shortcut**: Press `Ctrl + M`.
   - **The Konami Code**: Unleash the hidden player by entering the legendary sequence!
     > **`↑` `↑` `↓` `↓` `←` `→` `←` `→` `B` `A` `ENTER`**

Upon first launch, the player will prompt you to authenticate with your Spotify account. Once authorized, the Mini Player will load your current playback state and grant you full control over your active devices.

## Architecture and Security

- **PKCE Authentication**: The userscript utilizes Proof Key for Code Exchange (PKCE). This means no Client Secret is ever exposed or required in the frontend code.
- **Sandboxed Execution**: Authentication and token storage happen securely within the Tampermonkey sandbox, preventing standard scripts on the host page from accessing your tokens.
- **Real-Page Bridge**: The script injects a lightweight bridge into the true window context to communicate with the official Spotify Web Playback SDK using secure event dispatching.
