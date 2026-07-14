# What's new in Apotheosis

A running log of what's changed, newest first. If you're on a TestFlight build and want to know what to look for, start here.

## 0.9.0 (5) · 2026-07-01

**Apple TV joins the beta, and so do Jellyfin and Plex servers.**

This is the big one. Apotheosis is now a tvOS app as well as an iPhone and iPad app, built from the ground up for the remote rather than ported from touch. Same TestFlight build, same Universal Purchase, so installing on Apple TV costs nothing extra. Two new server types come along for the ride.

- **Apple TV.** Discovery, library grids, search, detail pages, Settings, and a full Live TV guide, all focus-driven for the remote. Sign in on your iPhone and push the connection to the Apple TV (no typing server URLs with the on-screen keyboard).
- **A player that direct-plays your files on Apple TV.** 4K HDR, HEVC 10-bit, and MKV play without transcoding, off both Emby and IPTV. Auto-play-next for binges and an in-player episode picker are built in.
- **Plex.** Sign in with your Plex account and browse your movie and TV libraries. Continue Watching picks up right alongside Emby and IPTV, and you get the same detail pages, cast rail, and direct-play player as every other source. (Plex Live TV/DVR and Favorites sync are still to come.)
- **Jellyfin.** Add a Jellyfin server from the same Media Server screen as Emby. The app detects which one you're connecting to. This is early support, so kick the tires and report anything off.
- Series version switching no longer trips over itself when a show has more than one copy, and it keeps your place in the episode when you switch.
- "Couldn't load episodes" now offers a Retry instead of a dead end (Emby and Plex).
- Seeking on large 4K files is steadier, with a recovery path if the stream stalls mid-scrub.
- "See All" on a huge library loads in pages as you scroll instead of trying to render everything at once.
- Switching between servers no longer leaves the previous server's artwork lingering on the home screen.

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
- Bug reports can carry a redacted log when "Include Logs" is on. Scrubbed on your device before sending, goes only to the developer, never the public tracker. If the app restarts unexpectedly, the report now also carries the log from *before* the restart, so crashes are far easier to track down.

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
