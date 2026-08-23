# What's new in Apotheosis

A running log of what's changed, newest first. If you're on a TestFlight build and want to know what to look for, start here.

## 0.9.0 (11) · 2026-08-23

**Series rails that paint instead of hanging, Custom Rail editors that hide empty axes, and a month of Continue Watching / Skip Intro manners from the soak.**

Same soak as 0.9.0 (10). Build 10 was cut locally and expired unused so TestFlight could take 11.

- **Series filter rails.** Grouping is O(n) again. A Documentary rail that used to lock the tab now appears whole.
- **Apple TV Custom Rails.** Empty axes hide after the catalog lands. An empty picker focuses Close; Menu dismisses the sheet instead of the app.
- **Skip Intro / CrowdSkip.** Crowd windows win over name-heuristic and typed-server chapters; mega-season shows remap to absolute episode numbers.
- **Continue Watching.** Nil LastPlayedDate no longer steals the rail; web scrub updates resume; Remove stays off the app rail (web may still show it).
- **Playback residuals.** Dual-audio MKV lead-in sync (vendor #19); stub-`avcC` black screen (vendor #18); series stills / synopsis; Oblivion backdrop.

## 0.9.0 (10) · 2026-08-21

_Expired unused 2026-08-23. Same notes shipped as 0.9.0 (11)._

Soak cut after living on `main` past 0.9.0 (9). Highlights:

- **Series filter rails.** Grouping is O(n) again. A Documentary rail that used to lock the tab now appears whole.
- **Apple TV Custom Rails.** Empty axes hide after the catalog lands. An empty picker focuses Close; Menu dismisses the sheet instead of the app.
- **Skip Intro / CrowdSkip.** Crowd windows win over name-heuristic and typed-server chapters; mega-season shows remap to absolute episode numbers.
- **Continue Watching.** Nil LastPlayedDate no longer steals the rail; web scrub updates resume; Remove stays off the app rail (web may still show it).
- **Playback residuals.** Dual-audio MKV lead-in sync (vendor #19); stub-`avcC` black screen (vendor #18); series stills / synopsis; Oblivion backdrop.

## 0.9.0 (9) · 2026-07-31

**Playback continuity after app-switch, calmer episode endings, clear logos, and binge-exit focus.**

Polish-lab merge to `main`. Highlights:

- **Background / app-switch.** Aether reloads and reasserts play when you leave and come back; open-window resign no longer races the first load on iPhone.
- **Episode endings.** Post-credits false EOF gated; near-end demux walls drain like a normal end instead of freeze/skip/die. Audio language survives reloads.
- **Binge exit.** After Next Episode + back, series detail lands on the episode you just left.
- **Clear logos.** Smart ranking + Settings source control; padded canvases trimmed on display.
- **See-All / volume / titles.** Option A viewport no-bounce; iOS portrait volume HUD expands on hardware buttons; remux filename episode titles cleaned with TMDB fallback.

## 0.9.0 (8) · 2026-07-25

**Hotfix: Apple TV Favorites See-All pages reliably; sibling versions consolidate again.**

- **Favorites load-more + sibling UX.** Paging uses raw Emby `StartIndex` / full-page `hasMore` / mount+tail prefetch (`1f89d53`→`48464ab`→`c9a4e83` + restore). Display consolidates version siblings again on Movies+Series Favorites See-All (skip-consolidate was a temporary load-more lever). Device-verify owed on TF. Tip stays build **8** (never archived).

## 0.9.0 (7) · 2026-07-24

**Player chrome cleaned up, Live TV stays up through splices, and Apple TV scrubbing / See-All feel less brittle.**

Cut A for this week, plus the open items that landed on `main` before the upload. Highlights:

- **Tracks / Navigate / More.** Chapters live under Navigate on phone and Apple TV, not buried in gear. Skip Intro clears above the chrome cluster; text subs sit nearer the scrub stack.
- **Live TV recovery + splice freeze.** When a live producer wedges, the host falls back to HLS. Mid-stream quality / SPS changes rotate the fMP4 init so video doesn't freeze ([public #22](https://github.com/peewee5/apotheosis-public/issues/22)).
- **Apple TV rapid VOD scrub.** Chrome coalesces seeks while a prior seek is still landing — no more stacked buffering storm ([public #27](https://github.com/peewee5/apotheosis-public/issues/27)).
- **Trakt foundation.** Device OAuth + Keychain + DEBUG Connect. Full history sync is next.
- **Emby playlists.** Create and reorder on iPhone; Add on Apple TV. Large-playlist confirm still welcome.
- **Favorites / See-All.** Sibling-aware hearts across See All, custom rails, and Search; scrubber clamped to mounted posters; bounded poster windows for huge libraries.
- **Previous-session logs after force-quit.** Session logs flush on resign / background (batched FileHandle sync) so a previous-session crash report still carries the lead-up ([public #28](https://github.com/peewee5/apotheosis-public/issues/28), [public #29](https://github.com/peewee5/apotheosis-public/issues/29)).

## 0.9.0 (6) · 2026-07-17

**TMDB enrichment, steadier scrubbing, Skip Intro crowd lookup, and a long list of Apple TV focus / discovery fixes.**

This cut looked small in the first release-notes draft; the window after (5) actually carried a full polish + engine pass. Highlights:

- **Optional TMDB enrichment (bring your own key).** Clear logos, cast, and thinner-artwork rescue when the server metadata is sparse.
- **Scrubbing is much harder to break.** Aggressive backward seek on VOD no longer piles into a stuck-paused `-1008` state ([public #23](https://github.com/peewee5/apotheosis-public/issues/23)). Custom scrub bar + tap-to-seek behave as you’d expect.
- **Skip Intro / Credits crowd lookup.** TheIntroDB and IntroDB.app as an opt-in fallback when the server has no markers.
- **Emby chapters from every Play path** that should have them (CW, long-press, library, Search — not only detail Play).
- **Home / discovery feel.** Warm Movies ↔ Series tab switches keep decoded artwork; discovery no longer flashes a spinner over cached rails; a pile of tvOS focus, hero, and clear-logo fixes.
- **Player options panel layout.** Orientation chips no longer overlap Subtitle Style; rows left-align with the panel.
- Interlaced H.264 deinterlaces via the software path; sidecar subtitles capped at 1 MB; Settings / About polish on Apple TV.

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
