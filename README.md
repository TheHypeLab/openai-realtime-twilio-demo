# OpenAI Realtime API with Twilio Quickstart

Combine OpenAI's Realtime API and Twilio's phone calling capability to build an AI calling assistant.

## Quick Setup

Open three terminal windows:

| Terminal | Purpose                       | Quick Reference                     |
| -------- | ----------------------------- | ----------------------------------- |
| 1        | To run the `webapp`           | `cd webapp && npm run dev`          |
| 2        | To run the `websocket-server` | `cd websocket-server && npm run dev`|
| 3        | To run `ngrok`                | `ngrok http 8081`                   |

Make sure all vars in `webapp/.env` and `websocket-server/.env` are set correctly.

## Setup Instructions

1. Install dependencies for all components:
   ```
   npm run install:all
   ```

2. Set up your environment variables:
   - In `webapp/.env`, add your Twilio credentials:
     ```
     TWILIO_ACCOUNT_SID="your_twilio_sid"
     TWILIO_AUTH_TOKEN="your_twilio_auth_token"
     ```
   - In `websocket-server/.env`, add your OpenAI API key and public URL:
     ```
     OPENAI_API_KEY="your_openai_api_key"
     PUBLIC_URL="your_ngrok_url"
     ```

3. Start ngrok to expose your local server:
   ```
   ngrok http 8081
   ```
   Copy the forwarding URL (e.g., `https://abc123.ngrok-free.app`) and set it as your `PUBLIC_URL` in `websocket-server/.env`.

4. Start the webapp and websocket server:
   ```
   npm run dev
   ```
   Or start them individually:
   ```
   cd webapp && npm run dev
   cd websocket-server && npm run dev
   ```

5. Follow the setup checklist in the webapp to configure your Twilio phone number.

## Overview

This project implements a phone calling assistant with the OpenAI Realtime API and Twilio, and has two main parts:

1. `webapp`: NextJS app to serve as a frontend for call configuration and transcripts
2. `websocket-server`: Express backend that handles connection from Twilio, connects it to the Realtime API, and forwards messages to the frontend

Twilio uses TwiML to specify how to handle a phone call. When a call comes in, we tell Twilio to start a bi-directional stream to our backend, where we forward messages between the call and the Realtime API.