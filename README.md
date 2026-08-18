# Handoff

A minimal peer-to-peer file transfer web app using WebRTC DataChannel.

Files are transferred directly between the two browsers after a manual
offer/answer exchange. No application server is used to store or route files.

## Features

- Browser-to-browser file transfer using WebRTC DataChannel
- Manual connection-code exchange
- Drag-and-drop file selection
- Transfer progress indicator
- No login or application database
- Static-site compatible; suitable for GitHub Pages
- Responsive dark UI

## How it works

1. One user selects **Create connection**.
2. The generated WebRTC offer is copied to the other user.
3. The second user selects **Join connection**, pastes the offer, and generates an answer.
4. The answer is copied back to the first user.
5. Once the WebRTC DataChannel opens, either side can send a file.

The application uses a public Google STUN server only for ICE candidate discovery:

`stun:stun.l.google.com:19302`

STUN helps browsers discover network connectivity information. It does not
carry the file payload. Depending on the networks involved, a direct
peer-to-peer connection may not always be possible without a TURN relay.

## Run locally

A local HTTP server is recommended:

```bash
python -m http.server 8000
```

Then open:

http://localhost:8000

For deployment, use HTTPS. WebRTC functionality and browser security policies
are best supported from a secure origin.

## Deploy with GitHub Pages

1. Create a GitHub repository, for example `handoff`.
2. Upload `index.html` and this `README.md`.
3. In **Settings → Pages**, select the deployment source.
4. Open the generated HTTPS GitHub Pages URL in both browsers.

## Security notes

- The application does not upload files to an application server.
- WebRTC provides encrypted transport for the data channel.
- The connection offer/answer contains WebRTC session information and should
  be exchanged through a channel you trust.
- This project does not provide identity verification or end-to-end application
  authentication beyond WebRTC's transport security.
- Closing the browser tab ends the current session; the app itself does not
  maintain a persistent file store.

## Project structure

```text
handoff/
├── index.html
├── README.md
├── LICENSE
└── .gitignore
```

## License

MIT License. See `LICENSE`.
