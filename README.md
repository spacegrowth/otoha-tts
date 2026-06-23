# Otoha TTS

Read the current note aloud in Obsidian, highlighting each sentence in place and
smooth-scrolling to follow the spoken line.

Works **standalone** with your device's built-in speech (no setup, no server, works
offline and on mobile). For higher-quality neural voices you can optionally point it
at a local [Kokoro](https://github.com/hexgrad/kokoro) server — fully local, no cloud.

## Features

- Read the whole note, the current selection, or from the cursor.
- In-place sentence highlighting that follows along as it reads.
- Smooth "teleprompter" auto-scroll that keeps the spoken line in view.
- Click any sentence while reading to jump there; play / pause / stop.
- Two engines: **Device** (built-in OS speech, default, offline) or **Kokoro**
  (a local server you run yourself).

## Install

**From the community plugins browser** (once listed): Settings → Community plugins →
Browse → search "Otoha TTS" → Install → Enable.

**Manually:** download `main.js`, `manifest.json`, and `styles.css` from the
[latest release](https://github.com/spacegrowth/otoha-tts/releases/latest) into
`<vault>/.obsidian/plugins/otoha-tts/`, then enable the plugin.

## Engines

- **Device** (default): uses the OS built-in speech synthesis. Nothing to install.
- **Kokoro**: set the engine to Kokoro in settings and run a local Kokoro HTTP server
  at `http://127.0.0.1:8765`. See [Otoha](https://github.com/spacegrowth/otoha) for a
  one-click menu-bar app that bundles and manages this server.

## Network use (full disclosure)

This plugin only ever talks to **localhost** — it makes no external/internet requests:

- **Kokoro engine:** HTTP requests to `http://127.0.0.1:8765` (only when you choose the
  Kokoro engine) to synthesize audio.
- **Companion app integration (desktop only):** to let the optional Otoha menu-bar app
  mirror and control playback, the plugin opens a small loopback HTTP listener on
  `127.0.0.1:8767` and posts playback state to `127.0.0.1:8766`. These bind to localhost
  only and are best-effort (skipped if the port is busy or unavailable, e.g. on mobile).

No telemetry, no analytics, no remote code.

## Development

Plain JS, no build step. Pure logic (sentence parsing, text matching, scroll math) has
unit tests:

```bash
npm test
```

## License

MIT — see [LICENSE](LICENSE).
