# Local voice API (STT + TTS)

I wanted speech-to-text and text-to-speech endpoints that behaved exactly like the OpenAI audio API, so any client written against OpenAI would "just work" — but running entirely on my own hardware instead of shipping every recording off to someone else's server.

  It's a small **FastAPI** service that exposes the OpenAI-shaped audio routes (`/v1/audio/transcriptions` and `/speech`) and backs them with local models:

  - **Speech-to-text** with `faster-whisper` (large-v3-turbo)
  - **Text-to-speech** with `Kokoro` (ONNX)

  ## The annoying part

  The transcription endpoint is easy until you meet real-world clients. Browsers send `webm`/`opus`, phones send `m4a`/`amr`/`3gp`, recorders send `wav`, and plenty of `mp3`/`flac`/`mpeg` in between — and `faster-whisper` doesn't want to deal with any of that container mess. So the service decodes whatever shows up into raw audio with **PyAV** before it ever reaches the model. It's not glamorous, but it's the reason the endpoint actually works when a random client points at it.

  Once that was handled, drop-in compatibility was the whole point: anything that talks to the OpenAI voice API works unchanged against this.
