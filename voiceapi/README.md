# Local voice API (STT + TTS)

FastAPI service exposing OpenAI-shaped audio routes (`/v1/audio/transcriptions`, `/speech`) over local models: faster-whisper (large-v3-turbo) STT, Kokoro (ONNX) TTS. PyAV decodes arbitrary input containers (webm/opus, m4a, wav, mp3, etc.) before whisper. Drop-in OpenAI-compatible.