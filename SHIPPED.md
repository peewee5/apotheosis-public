# What's new in Apotheosis

A running log of what's changed, newest first. If you're on a TestFlight build and want to know what to look for, start here.

## 0.9.0 (4) · 2026-05-31

**Big Live TV playlists done right, plus richer bug reports.**

- Huge channel lists (tens of thousands of channels) no longer crash the app. Large categories now open in a fast, scrollable browser instead of the full guide, so even a 30,000-channel playlist loads and scrolls smoothly.
- Browse those large lists as a grid or a plain list, your pick. The layout switch sits next to the category name and remembers your choice.
- EPG-linked M3U playlists show what's on now, with a progress bar, right in the large list and grid, not just in the guide.
- Bug reports can carry a redacted log when "Include Logs" is on. It's scrubbed on your device (no server addresses, credentials, or stream URLs) and goes only to the developer, never the public tracker, so problems are much faster to pin down.

## 0.9.0 (2) · 2026-05-30

**Safer connections, Tailscale support, and a better bug reporter.**

- Connections now default to secure (HTTPS with a valid certificate). If your server already uses HTTPS, nothing changes for you.
- Self-hosting over plain HTTP or a self-signed certificate on your home network? There's a new "Allow insecure connection" toggle in the Emby and XC setup screens. You opt in yourself, the server gets an "Unencrypted" badge in Settings, and the toggle only applies to servers on a local address.
- Already connecting to a local server over HTTP? It keeps working after the update. Nothing to reconfigure.
- Reaching a server over Tailscale works now. Use your machine's Tailscale name (the `*.ts.net` one), not the raw `100.x` address.
- Apotheosis remembers your Emby server's identity. A renewed certificate gets a quick heads-up; a different server answering at the same address stops and asks before trusting it.
- Bug reports can include an optional contact if you're open to follow-up. It stays private and never lands on the public tracker. You'll also get a short reference code after sending, in case you want to mention it later.

## 0.9.0 (1): first beta (2026-05-28)

First TestFlight build. One app for Emby, Xtream Codes (IPTV), and M3U playlists:

- Movies, Series, and Live TV together, with a Continue Watching row that follows you across sources.
- A Live TV guide built for big channel lists (tens of thousands).
- Two playback engines with automatic fallback when a file won't play, plus AirPlay and Picture in Picture.
- Optional iCloud sync for your saved logins. Off by default; turn it on in Settings → Sync.
- In-app bug reporting that strips out anything sensitive before it leaves your device.
