# What's new in Apotheosis

A running log of what's changed, newest first. If you're on a TestFlight build and want to know what to look for, start here.

## 0.9.0 (4) · 2026-06-01

**Live TV navigation rebuilt for the real world of massive IPTV playlists.**

Reseller IPTV playlists routinely dump 30,000 or more channels into a single category. Most clients become unusable at that scale. This build fixes that, then adds a round of polish across navigation, display, and bug reporting.

- Huge categories (over 1,500 channels) open in a purpose-built scrollable browser instead of the full guide, which runs out of memory trying to render 30,000 rows. Switch to any normal-sized category and the full guide returns automatically.
- Search in large channel sets is one tap away. Type a name and results filter instantly from the already-loaded list. No network call, no delay.
- Grid and list layout is now a single tap, not a menu. Quick Chips mode (channels vs. categories) is the same. Both toggles sit where they belong: layout next to the category name, chip mode in the toolbar.
- Channel tiles strip the encoding noise out of movie names. "War Machine 2026 [1080p] [BluRay]" becomes "War Machine 2026" with a small "1080p · BluRay" note below, so same-title entries at different qualities stay easy to tell apart.
- Custom channel names (set in Settings) now show everywhere: the guide, the large list, the large grid.
- Live channels in the large list and grid now show what is on now as you scroll, fetched gently in the background so even a huge playlist does not hammer your provider. (Movie and other on-demand entries stay clean, since they have no live schedule.)
- M3U playlists with XMLTV show what is on now, with a progress bar, right in the large list and grid.
- Bug reports can carry a redacted log when "Include Logs" is on. Scrubbed on your device before sending, goes only to the developer, never the public tracker.

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
