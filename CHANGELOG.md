# Changelog

All notable changes to Apotheosis are documented here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versioning
is `MARKETING_VERSION (CURRENT_PROJECT_VERSION)` — a marketing version plus a build
number that increments with every TestFlight cut, not strict Semantic Versioning (this
is a beta client app distributed via TestFlight, not a versioned library or API).

Headings stay Added / Changed / Fixed / Security. Optional area tag at the end of a
bullet (`_(Playback)_`, `_(Live TV)_`, `_(Discovery)_`, `_(Library)_`, `_(Settings)_`,
`_(Docs)_`) — skim aid only; skip on thin cuts.

See also [`SHIPPED.md`](SHIPPED.md).

**From in-app reports:** when a Worker-filed bug is fixed, link the **public** tracking
issue under that heading (never the private diagnostic twin). Public titles stay
generic until closed — retitle the public issue with a safe summary at close so the
changelog link is readable. The CI triage enricher runs on the **private** repo only
(by design: it reads redacted logs).

## [Unreleased]

_Draft for 0.9.0 (7) — landed on `main` after Build 6 shipped to TestFlight._

### Added

- Player chrome consolidation on iPhone and Apple TV: Tracks / Navigate / More (chapters
  live under Navigate, not buried in gear). _(Playback)_
- Trakt layer-1: device OAuth + Keychain storage + DEBUG Connect (full history sync still
  upcoming). Honors Trakt `slow_down` with capped backoff while polling. _(Library)_

### Fixed

- Text subtitles no longer sit mid-screen over the playback controls when chrome is up.
  _(Playback)_
- Skip Intro control cleared above the bottom chrome cluster after consolidation.
  _(Playback)_
- Host now consumes AetherEngine `liveSourceReset` and falls back to HLS AVPlayer when a
  live producer wedges (SSAI / no-cut stall class). Zap-fence so a disappearing player
  cannot start a late recovery. _(Live TV)_
- Favorites See-All: first-paint parity, toast-only load-more, stable Emby page order
  (no scramble while paging). _(Discovery)_
- Emby See-All / library sort: UI order threaded into server pagination. _(Discovery)_

### Changed

- iOS player chrome edge insets retuned on device (horizontal inset 40). _(Playback)_
- Docs / screenshots refresh for FEATURES and README (public mirror). _(Docs)_

## [0.9.0] - Build 6 - 2026-07-17

### Added

- Crowd Skip Intro / Credits lookup: TheIntroDB + IntroDB.app fallback (opt-in under
  Playback), wired for Emby and Plex direct-play. _(Playback)_
- Custom scrub bar (gesture-driven) with grow-on-touch feedback; tap-to-seek no longer
  swallowed by a no-op Slider drag. _(Playback)_
- Sidecar subtitle decode capped at 1 MB (network and local paths). _(Playback)_
- Optional TMDB online enrichment (BYOK): clear logos, cast, episode metadata, and hero
  backfill when server artwork is thin. _(Discovery)_
- Artwork cache controls; decoded-bitmap cache for warm Movies ↔ Series tab switches.
  _(Discovery)_

### Fixed

- VOD scrub / seek restart storm that could end in `NSURLErrorDomain -1008` and a stuck
  paused player — AetherEngine A10 bounded teardown-rebuild (see From in-app reports).
  _(Playback)_
- Emby movie chapters hydrate on Continue Watching, long-press / library Play, discovery
  hero Play, and Search — not only detail-page Play after `itemDetails` settles.
  _(Playback)_
- Chapters load-order race on iOS detail Play (generation-fenced). _(Playback)_
- Player options panel: Orientation chips no longer overlap Subtitle Style; chip rows
  and Mute / Chapters / Subtitle Style rows left-align with panel content. _(Playback)_
- Interlaced H.264 routed to the software decode path (deinterlace). _(Playback)_
- Auto-mark-watched leaving a stale Emby resume point; series auto-mark threshold 90%.
  _(Playback)_
- Discovery re-entry no longer shows a loading spinner over already-cached Movies /
  Series rails (including Plex / XC-category rails). _(Discovery)_
- Clear-logo flash / revert / SVG-undecodable TMDB logos; URL-cascade fallback
  (TMDB → Emby → text). _(Discovery)_
- tvOS focus: sidebar tab-reselect pops to root; CW-rail / hero focus steals and
  backdrop flash on warm tab switches; detail action cluster redesign. _(Discovery)_
- Series poster title/year display; Search casing/stills; genre counting and dead keys;
  custom-rail See-All source / axis parity; "On Demand" rail mixing sources.
  _(Discovery)_
- Detail-page plain-text title fallbacks use title casing (including tvOS Plex series).
  _(Discovery)_

### Changed

- Warm Movies ↔ Series tab switches reuse decoded poster/hero bitmaps via an in-memory
  `CachedAsyncImage` cache (Clear Artwork Cache still clears it). _(Discovery)_
- Custom rails cache `customRailItems` to cut tab-switch body cost. _(Discovery)_
- tvOS Settings / About polish (Report an Issue or Idea; Quick Diagnostic at bottom of
  About; Media Server Plex link copy). _(Settings)_
- Bug-report free-text shows a §4.4 credential-paste reminder. _(Settings)_

### From in-app reports

- [VOD scrub seek freeze (stuck paused)](https://github.com/peewee5/apotheosis-public/issues/23)
  — fixed by AetherEngine A10 bounded teardown-rebuild. _(Playback)_

## [0.9.0] - Build 5 - 2026-07-01

### Added

- Apple TV platform support: discovery, library grids, search, detail pages, Settings,
  and a full Live TV guide, all focus-driven for the remote.
- A direct-play video engine on Apple TV (4K HDR, HEVC 10-bit, MKV, no transcode) off
  both Emby and IPTV, with auto-play-next and an in-player episode picker.
- Plex support: sign in with a Plex account, browse movie and TV libraries, Continue
  Watching (On Deck) alongside Emby and IPTV, cast/crew, and direct-play.
- Jellyfin support (early): auto-detected from the same Media Server screen as Emby.

### Fixed

- Series version switching no longer breaks on shows with more than one copy, and
  resume position now survives a version switch.
- "Couldn't load episodes" now offers a Retry instead of a dead end (Emby and Plex).
- Seeking on large 4K files is steadier, with a recovery path if the stream stalls
  mid-scrub.
- "See All" on a large library now paginates as you scroll instead of attempting to
  render the entire library at once.
- Switching servers no longer leaves the previous server's artwork lingering on the
  home screen.

## [0.9.0] - Build 4 - 2026-06-01

### Added

- Large Live TV categories (over ~1,500 channels) open in a dedicated scrollable
  browser instead of the full EPG grid, which ran out of memory past that scale.
  Normal-sized categories still get the full guide automatically.
- Instant local search across large channel sets (filters the already-loaded list,
  no network round trip).
- Live "on now" indicators in the large channel list/grid, fetched in the background
  so a large playlist doesn't hammer the provider; M3U + XMLTV playlists get the same
  treatment with a progress bar.
- Bug reports can optionally attach a redacted log ("Include Logs"), scrubbed on-device
  before sending. If the app restarted unexpectedly, the report also carries the
  previous session's log.

### Changed

- Grid/list layout toggle and Quick Chips mode (channels vs. categories) are now a
  single tap instead of a menu, and both live where they belong (layout next to the
  category name, chip mode in the toolbar).
- Channel tiles strip encoding noise from titles (e.g. "War Machine 2026 [1080p]
  [BluRay]" becomes "War Machine 2026" with a small "1080p · BluRay" note below), so
  same-title entries at different qualities stay easy to tell apart.
- Custom channel names (set in Settings) now show consistently across the guide, the
  large list, and the large grid.

## [0.9.0] - Build 2 - 2026-05-30

### Security

- Connections now default to secure (HTTPS with a valid certificate).
- Self-hosted servers on plain HTTP or a self-signed certificate can opt in via a new
  "Allow insecure connection" toggle on the Emby/XC setup screens — explicit, per-server,
  and only available for servers on a local address. An "Unencrypted" badge shows in
  Settings for any server using it.
- Apotheosis now remembers a connected Emby server's identity: a renewed certificate on
  the same server gets a quiet heads-up; a different server answering at the same
  address stops and asks for confirmation before trusting it.

### Added

- Support for reaching a self-hosted server over Tailscale (`*.ts.net` name).
- Bug reports can include an optional contact for follow-up (private, never on the
  public tracker) and now return a short reference code after sending.

## [0.9.0] - Build 1 - 2026-05-28

First TestFlight build.

### Added

- Movies, Series, and Live TV in one app for Emby, Xtream Codes (IPTV), and M3U
  playlists, with a Continue Watching row that follows the user across sources.
- A Live TV guide built for large channel lists (tens of thousands of channels).
- Two playback engines with automatic fallback when a file won't play, plus AirPlay
  and Picture in Picture.
- Optional iCloud sync for saved logins (off by default, Settings → Sync).
- In-app bug reporting that strips sensitive data before it leaves the device.
