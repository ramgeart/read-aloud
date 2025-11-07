# Using OpenAI-Compatible TTS APIs

Read Aloud supports OpenAI's Text-to-Speech API and any OpenAI-compatible TTS endpoints. This allows you to use various TTS providers that implement the OpenAI API specification.

## Compatible Services

This feature works with:
- **OpenAI TTS API** - Official OpenAI text-to-speech service
- **LocalAI** - Self-hosted AI services with OpenAI-compatible endpoints
- **vLLM** - High-performance inference server with OpenAI API compatibility
- **Text Generation WebUI** - Self-hosted AI with OpenAI API extensions
- **Any other service** that implements the OpenAI `/v1/audio/speech` endpoint

## Configuration Steps

1. Click the Read Aloud icon on the Extensions menu
2. Stop any text that may be playing
3. Click on the Gear icon in the Read Aloud context menu
4. Select `Enable Custom Voices` in the "Voice" dropdown
5. In the Custom Voices window, find the **OpenAI** section
6. Click **Add** to configure a new OpenAI-compatible endpoint

## Configuration Options

### API URL
Enter the base URL of your TTS API endpoint. Examples:
- OpenAI: `https://api.openai.com/v1`
- LocalAI: `http://localhost:8080/v1`
- Custom endpoint: `https://your-tts-server.com/v1`

### API Key
Enter your API key if the service requires authentication. This field is optional for services that don't require authentication (like some self-hosted instances).

### Voice List
Define the available voices in JSON format. Each voice entry should include:
- `voice`: Voice identifier (required)
- `lang`: Language code (required, e.g., "en-US", "es-ES")
- `model`: TTS model to use (required, e.g., "tts-1", "tts-1-hd")
- `instructions`: Optional custom instructions for the voice

Example configuration:
```json
[
  {
    "voice": "alloy",
    "lang": "en-US",
    "model": "tts-1"
  },
  {
    "voice": "nova",
    "lang": "en-US",
    "model": "tts-1-hd"
  },
  {
    "voice": "custom-voice",
    "lang": "es-ES",
    "model": "tts-1",
    "instructions": "Speak slowly and clearly"
  }
]
```

## Testing Your Configuration

After entering your configuration, click **Save**. The extension will test the connection by calling the `/models` endpoint. If successful, your custom voices will appear in the voice selector with the prefix "OpenAI".

## Using Your Custom Voices

1. Return to the options page
2. In the "Voice" dropdown, look for voices prefixed with "OpenAI"
3. Select your desired voice
4. Adjust rate, pitch, and other settings as needed
5. Enjoy reading with your custom TTS service!

## Troubleshooting

### Connection Failed
- Verify the API URL is correct and accessible
- Check that the service is running (for self-hosted solutions)
- Ensure your API key is valid (if using authentication)

### Voice Not Working
- Confirm the voice name matches what's supported by your TTS service
- Check that the model name is correct for your service
- Verify the language code is in the correct format (e.g., "en-US" not "en")

### Permission Denied
- For self-hosted services on localhost, ensure your browser allows the extension to access local resources
- Check your API key has the necessary permissions

## API Compatibility Requirements

For a TTS service to work with Read Aloud, it must implement:
1. **POST** `/v1/audio/speech` endpoint that accepts:
   - `model`: The TTS model identifier
   - `input`: The text to synthesize
   - `voice`: The voice identifier
   - `response_format`: Audio format (extension uses "mp3")
   - `instructions`: Optional voice instructions

2. **GET** `/v1/models` endpoint (for configuration testing)

3. Return audio data in the specified format (MP3)
