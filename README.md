# Twilio OpenAI Realtime Voice Assistant

This project demonstrates how to create a voice assistant using Twilio's Programmable Voice API and OpenAI's Realtime API. It allows users to have a conversation with an AI assistant over a phone call.

## Features

- Real-time voice conversation with an AI assistant
- Integration with Twilio for handling phone calls
- Integration with OpenAI's Realtime API for AI responses
- WebSocket-based audio streaming
- Configurable AI personality and voice

## Prerequisites

- Node.js (v18+ or later recommended)
- A Twilio account with a phone number
- An OpenAI account with access to the Realtime API (beta)
- Homebrew (for macOS users)

## Installation

1. Clone this repository:
   ```
   git clone https://github.com/yourusername/twilio-openai-voice-assistant.git
   cd twilio-openai-voice-assistant
   ```

2. Install dependencies:
   ```
   npm install
   ```

3. Create a `.env` file in the root directory and add your API keys:
   ```
   OPENAI_API_KEY=your_openai_api_key_here
   PORT=5050
   TWILIO_ACCOUNT_SID=your_twilio_account_sid_here
   TWILIO_API_KEY=your_twilio_api_key_here
   TWILIO_API_SECRET=your_twilio_api_secret_here
   ```

4. Install and configure ngrok:
   ```
   brew install ngrok
   ngrok config add-authtoken your_ngrok_authtoken_here
   ```

5. Install Twilio CLI:
   ```
   brew tap twilio/brew && brew install twilio
   twilio version
   ```

6. Install Twilio Dev Phone plugin:
   ```
   twilio plugins:install @twilio-labs/plugin-dev-phone
   ```

## Configuration

- Modify the `SYSTEM_PROMPT` constant in `index.js` to change the AI assistant's personality and behavior.
- Adjust the `VOICE` constant to change the AI's voice (options: alloy, echo, fable, onyx, nova, shimmer).

## Usage

1. Load environment variables:
   ```
   export $(grep -v '^#' .env | xargs)
   ```

2. Start the server:
   ```
   npm start
   ```

3. In a new terminal, start ngrok:
   ```
   ngrok http 5050
   ```

4. In another terminal, start the Twilio Dev Phone:
   ```
   twilio dev-phone
   ```

5. Configure your Twilio phone number:
   - Go to the Twilio Console
   - Navigate to your phone number's configuration
   - Set the webhook for incoming calls to `https://your-ngrok-url/incoming-call`

6. Use the Twilio Dev Phone or call your Twilio phone number to start a conversation with the AI assistant.

## How It Works

1. When a call comes in, Twilio sends a webhook to the `/incoming-call` endpoint.
2. The server responds with TwiML instructions to connect the call to a WebSocket.
3. Audio from the call is streamed to the server via WebSocket.
4. The server forwards the audio to OpenAI's Realtime API.
5. Responses from the AI are streamed back to the caller in real-time.

## Limitations and Considerations

- This project is a demonstration and may not be suitable for production use without further development and security considerations.
- The OpenAI Realtime API is in beta and may change.
- Ensure compliance with relevant laws and regulations regarding AI, voice recording, and data privacy.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Twilio for their Programmable Voice API
- OpenAI for their Realtime API
- The open-source community for the various libraries used in this project
