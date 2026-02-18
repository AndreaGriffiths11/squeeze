# Squeeze 🍊

Drop a video, get it under your target file size. Runs 100% in your browser.

**Live:** [https://andreagriffiths11.github.io/squeeze](https://andreagriffiths11.github.io/squeeze)

## ✨ Features

- **100% Client-Side** — Nothing gets uploaded. All processing happens in your browser
- **Smart Compression** — Automatically calculates optimal bitrate based on target size and video duration
- **Multiple Formats** — Supports both MP4 (H.264) and WebM (VP8) output
- **Real-Time Progress** — See encoding progress with live status updates
- **Zero Dependencies** — Single HTML file, no build process required
- **Privacy First** — Your videos never leave your device

## 🚀 How it works

1. Drop or select a video file
2. Set your target file size (in MB)
3. Choose output format (MP4 or WebM)
4. Click compress and watch the magic happen
5. Download your compressed video

Under the hood:
- Uses [FFmpeg WASM](https://github.com/ffmpegwasm/ffmpeg.wasm) to compress videos entirely client-side
- Calculates optimal bitrate from your target size and the video's duration
- Encodes using libx264 (MP4) or libvpx (WebM) with AAC/Vorbis audio
- Nothing gets uploaded anywhere — complete privacy

## 🛠️ Stack

- Single `index.html` file (no build tools needed!)
- Vanilla JavaScript (ES6 modules)
- FFmpeg WASM v0.12.15 (loaded from CDN)
- [coi-serviceworker](https://github.com/nicoth-in/coi-serviceworker) for `SharedArrayBuffer` support on GitHub Pages

## 💻 Run locally

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

> **Note:** The custom headers (`Cross-Origin-Opener-Policy` and `Cross-Origin-Embedder-Policy`) are required for `SharedArrayBuffer` support, which FFmpeg WASM needs to function.

## 🌐 Deploy to GitHub Pages

1. Push to GitHub
2. Go to Settings → Pages
3. Set Source to `main` branch, root `/`
4. Done! Your site will be live at `https://yourusername.github.io/squeeze`

The `coi-serviceworker.js` file (loaded from CDN) automatically adds the required headers for GitHub Pages.

## 🌍 Browser Support

Requires a modern browser with `SharedArrayBuffer` support:

- ✅ Chrome 68+
- ✅ Edge 79+
- ✅ Firefox 79+ (with `dom.postMessage.sharedArrayBuffer.bypassCOOP_COEP.insecure.enabled` set to `true` in about:config)
- ✅ Safari 15.2+
- ❌ Mobile browsers (limited support)

## ⚠️ Limitations

- **Performance:** Encoding can be slow for large videos or high bitrates (it's running FFmpeg in your browser!)
- **Memory:** Large video files may consume significant memory during processing
- **SharedArrayBuffer:** Requires proper headers, which is handled automatically via the service worker on GitHub Pages
- **File Size:** Very large input files (>500MB) may cause issues depending on your device's available RAM

## 🤝 Contributing

Contributions are welcome! This is a simple single-file project, so there's no complex setup required.

1. Fork the repository
2. Make your changes to `index.html`
3. Test locally using one of the methods above
4. Submit a pull request

## 📝 License

MIT License - see [LICENSE](LICENSE) file for details

## 🙏 Credits

- [FFmpeg WASM](https://github.com/ffmpegwasm/ffmpeg.wasm) - Making FFmpeg run in the browser
- [coi-serviceworker](https://github.com/nicoth-in/coi-serviceworker) - Enabling SharedArrayBuffer on GitHub Pages

## 💡 Use Cases

- Compress videos before emailing
- Reduce file size for social media uploads
- Quick video format conversion
- Privacy-conscious video processing (nothing leaves your browser)
- Learning how FFmpeg WASM works

---

Built with ❤️ using pure JavaScript and FFmpeg WASM
