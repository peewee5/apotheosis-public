# What's new in Apotheosis

A running log of what's changed, newest first. If you're on a TestFlight build and want to know what to look for, start here.

## Unreleased (next TestFlight build)

**How Apotheosis connects to your servers got safer.**

- Connections now default to secure (HTTPS with a valid certificate). If your server already uses HTTPS, nothing changes for you.
- Self-hosting over plain HTTP or a self-signed certificate on your home network? There's a new "Allow insecure connection" toggle in the Emby and XC setup screens. You opt in yourself, the server gets an "Unencrypted" badge in Settings, and the toggle only applies to servers on a local address.
- Already connecting to a local server over HTTP? It keeps working after the update. Nothing to reconfigure.
- Apotheosis now remembers your Emby server's identity. If its certificate gets renewed, you'll see a quick "certificate updated" note and that's it. If a different server ever answers at the same address, the app stops and asks before trusting it.

## 0.9.0 (1): first beta (2026-05-28)

First TestFlight build. One app for Emby, Xtream Codes (IPTV), and M3U playlists:

- Movies, Series, and Live TV together, with a Continue Watching row that follows you across sources.
- A Live TV guide built for big channel lists (tens of thousands).
- Two playback engines with automatic fallback when a file won't play, plus AirPlay and Picture in Picture.
- Optional iCloud sync for your saved logins. Off by default; turn it on in Settings → Sync.
- In-app bug reporting that strips out anything sensitive before it leaves your device.
