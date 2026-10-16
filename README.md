# Xiolim Video Metadata Studio — v2

Responsive static website for editing supported embedded video metadata using FFmpeg WebAssembly in the browser.

## Features
- Responsive dark UI with Xiolim developer branding.
- User-provided Catbox video embedded as a decorative hero preview.
- Select/drop a local video and inspect basic file metadata.
- Load FFmpeg WebAssembly on demand and show progress.
- Edit supported tags: title, comment, artist/creator, creation_time.
- Option to remove old global metadata before writing new tags.
- Real processing and video download using stream copy (`-c copy`), not re-encoding.

## Run
Because the app uses JavaScript modules and WebAssembly, serve it via HTTPS or a local server, rather than opening `index.html` as `file://`.

```bash
python -m http.server 8000
```
Open `http://localhost:8000`.

For deployment, upload the folder to static hosting such as Vercel or GitHub Pages. No build command is required; the project root is the output directory.

## Limitations
- FFmpeg WebAssembly is downloaded from public CDNs when the user clicks Load processing engine; internet is required.
- Browser memory limits can prevent processing very large videos, especially on mobile.
- Tag support depends on container/codec. The app retains the input extension and uses stream copy. Some containers may ignore tags or fail to mux the output.
- `-c copy` avoids video/audio re-encoding, so encoded stream quality is not reduced by re-encoding. Some container-specific metadata/atoms may still change or be dropped.
- Metadata editing does not guarantee that social platforms will treat a repost as original or bypass moderation/duplicate-content systems.
