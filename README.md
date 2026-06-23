# Otoha TTS

Read the current note aloud in Obsidian, highlighting each sentence in place and
smooth-scrolling to follow the spoken line.

Works **standalone** with your device's built-in speech (no setup, no server, works
offline and on mobile). For higher-quality neural voices, install the free
**[Otoha app](https://github.com/spacegrowth/otoha)** — a menu-bar app that bundles and
runs everything locally (no cloud, no accounts).

## Features

- Read the whole note, the current selection, or from the cursor.
- In-place sentence highlighting that follows along as it reads.
- Smooth "teleprompter" auto-scroll that keeps the spoken line in view.
- Click any sentence while reading to jump there; play / pause / stop.
- Two engines: **Device** (built-in OS speech, default, offline) or **Otoha**
  (high-quality neural voices via the free Otoha app — all local).

## Install

**From the community plugins browser** (once listed): Settings → Community plugins →
Browse → search "Otoha TTS" → Install → Enable.

**Manually:** download `main.js`, `manifest.json`, and `styles.css` from the
[latest release](https://github.com/spacegrowth/otoha-tts/releases/latest) into
`<vault>/.obsidian/plugins/otoha-tts/`, then enable the plugin.

## Engines

- **Device** (default): uses the OS built-in speech synthesis. Nothing to install,
  works offline and on mobile.
- **Otoha (neural voices):** install the free **[Otoha app](https://github.com/spacegrowth/otoha)**
  ([download](https://github.com/spacegrowth/otoha/releases/latest)). It runs a local
  [Kokoro](https://github.com/hexgrad/kokoro) server on your machine and the plugin talks
  to it at `http://127.0.0.1:8765` — all local, no cloud. Then pick the Kokoro engine in
  the plugin settings. (Advanced: you can run your own Kokoro server on that port instead
  of the app.)

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
