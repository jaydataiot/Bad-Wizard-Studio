# Malgrin Oracle interface

Professional standalone front end for the existing Malgrin Oracle service.

## Run locally

```sh
python3 -m http.server 4177
```

Open `http://127.0.0.1:4177/`.

## API connection

The page uses the existing Oracle endpoints:

- `POST /api/oracle/conversations`
- `POST /api/oracle/conversations/:id/messages` (SSE streaming response)
- `POST /api/oracle/tts`

When the page is hosted on `wizard-chat-assistant.replit.app`, requests remain same-origin. On other hosts, the page uses the origin configured on the `<html data-api-base="…">` attribute. The API must allow that site's origin and credentialed requests.

## Deployment

Copy `index.html` and the `assets` directory into the Replit app's public/static directory. If deploying beneath `/malgrin-oracle/`, make sure the web server returns this file for that route and does not overwrite the relative `assets/` paths.

The interface includes typed chat, streaming transcript updates, TTS playback, browser speech recognition, quick prompts, keyboard controls, mobile layouts, visible connection states, and accessible labels.

Audio playback uses one cancellable Web Audio channel. Starting another prompt stops prior narration, and mute immediately cancels both active audio and pending TTS requests. Malgrin's mouth movement is driven by the narration waveform through a Web Audio analyser.
