# Squeeze 🍊

Drop a video, get it under your target file size. Runs 100% in your browser — nothing gets uploaded anywhere.

**Live:** [https://andreagriffiths11.github.io/squeeze](https://andreagriffiths11.github.io/squeeze)

![Squeeze compressing a video](screenshot.png)

## Features

- Set a target file size (e.g. 9 MB) and Squeeze calculates the optimal bitrate
- Two-pass encoding with lanczos downscaling for the best quality at your target size
- Auto-downscales resolution when the bitrate is too low for the source (no point keeping 4K at 500kbps)
- Supports MP4 and WebM output
- Works with large files (2GB+) via WORKERFS zero-copy mounting
- Falls back to single-threaded mode when SharedArrayBuffer is unavailable

## How it works

1. You drop a video and set your target size
2. Squeeze probes the video duration with FFmpeg
3. It calculates the video bitrate needed to hit your target: `(targetMB * 8 * 1024) / durationSec - audioBitrate`
4. FFmpeg compresses the video in-browser using libx264 (MP4) or libvpx (WebM)
5. You download the result — nothing ever leaves your machine

## Stack

- Single `index.html` file, no build step
- [FFmpeg WASM](https://github.com/ffmpegwasm/ffmpeg.wasm) loaded from CDN (multi-threaded when possible, single-threaded fallback)
- [coi-serviceworker](https://github.com/nicoth-in/coi-serviceworker) for SharedArrayBuffer support on GitHub Pages

## Run locally

```bash
npx serve .
```

Then open `http://localhost:3000`

## Deploy

Push to GitHub, then Settings → Pages → Source: `main` branch, root `/`. Done.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

[MIT](LICENSE) — free to use, modify, and distribute with attribution.

---

Built by [Andrea Griffiths](mailto:andrea@mainbranch.com). For more projects and ideas, subscribe to my [newsletter](https://mainbranch.beehiiv.com/).
