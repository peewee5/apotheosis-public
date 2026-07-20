# Changelog

All notable changes to Apotheosis are documented here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versioning
is `MARKETING_VERSION (CURRENT_PROJECT_VERSION)` — a marketing version plus a build
number that increments with every TestFlight cut, not strict Semantic Versioning (this
is a beta client app distributed via TestFlight, not a versioned library or API).

For narrative, human-voiced release notes ("what to look for in this build"), see
[`SHIPPED.md`](SHIPPED.md) — this file covers the same releases in a stricter,
categorized format.

## [Unreleased]

## [0.9.0] - Build 6 - 2026-07-17

### Fixed

- Emby movie chapters now hydrate on Continue Watching, long-press / library Play,
  discovery hero Play, and Search — not only detail-page Play after `itemDetails`
  settles.
- Discovery re-entry no longer shows a loading spinner over already-cached Movies /
  Series rails while a background refresh runs.
- Player options panel: Orientation chips no longer overlap Subtitle Style; chip rows
  and Mute / Chapters / Subtitle Style rows left-align with panel content.
- Detail-page plain-text title fallbacks (no clear logo) use title casing, including
  the tvOS Plex series surface.

### Changed

- Warm Movies ↔ Series tab switches reuse decoded poster/hero bitmaps via an in-memory
  `CachedAsyncImage` cache (Clear Artwork Cache still clears it).
- tvOS About: "Report an Issue or Idea" copy; Submit Quick Diagnostic moved to the
  bottom of the list.

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
