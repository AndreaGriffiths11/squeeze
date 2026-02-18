# Squeeze 🍊

Drop a video, get it under your target file size. Runs 100% in your browser.

**Live:** [https://YOUR_USERNAME.github.io/squeeze](https://YOUR_USERNAME.github.io/squeeze)

## How it works

- Uses [FFmpeg WASM](https://github.com/ffmpegwasm/ffmpeg.wasm) to compress videos entirely client-side
- Calculates optimal bitrate from your target size and the video's duration
- Nothing gets uploaded anywhere

## Stack

- Single `index.html` file
- FFmpeg WASM (loaded from CDN)
- [coi-serviceworker](https://github.com/nicoth-in/coi-serviceworker) for `SharedArrayBuffer` support on GitHub Pages

## Run locally

```bash
# Option 1: npx
npx serve .

# Option 2: python
python3 -c "
import http.server
class H(http.server.SimpleHTTPRequestHandler):
    def end_headers(self):
        self.send_header('Cross-Origin-Opener-Policy','same-origin')
        self.send_header('Cross-Origin-Embedder-Policy','require-corp')
        super().end_headers()
http.server.HTTPServer(('',3000),H).serve_forever()
"
```

Then open `http://localhost:3000`

## Deploy

Push to GitHub, then Settings → Pages → Source: `main` branch, root `/`. Done.
