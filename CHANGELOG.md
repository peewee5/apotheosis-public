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
(by design: it reads redacted logs). Full close checklist (repos, §4.4 forbidden list,
never mirror enriched private titles): [`docs/PUBLIC_ISSUE_CLOSE_RITUAL.md`](docs/PUBLIC_ISSUE_CLOSE_RITUAL.md).

## [Unreleased]

_Empty — next cut after 0.9.0 (11)._

## [0.9.0] - Build 11 - 2026-08-23

Same soak as Build 10. Build 10 was cut locally and expired unused so TestFlight could take 11.

### Fixed

- Series filter rails no longer lock the UI: `LibraryConsolidator` Series grouping is O(n) again (key-bucketed union). Documentary / multi-genre rails paint whole on first appearance. _(Discovery)_
- Apple TV Custom Rail editor: empty content axes hide after the catalog lands (match iOS); an empty picker gets a focusable Close instead of Menu exiting the app. Search-miss seats Close and does not yank focus back to the first row. _(Settings)_
- Series Continue Watching: episodes with no LastPlayedDate sink instead of winning the rail. _(Discovery)_
- Skip Intro prefers crowd windows over Emby typed / name-heuristic chapters; CrowdSkip remaps mega-season shows to absolute episode numbers. _(Playback)_
- AAC stream-copy lead-in A/V desync on dual-audio MKV (vendor #19 silence bridge). _(Playback)_
- Emby VOD black screen + audio on stub `avcC` (vendor #18). _(Playback)_
- Series detail synopsis + episode stills (TMDB aired-order remap for mega-seasons). _(Discovery)_
- Oblivion-class blank Emby movie backdrop (client image path, not server homework). _(Discovery)_
- In-progress web scrub / mark-as-watched now updates Continue Watching resume instead of a false checkmark. _(Discovery)_

### Changed

- Remove from Continue Watching keeps the title off the app rail (sticky hide). Emby web can still show it until HideFromResume — not this cut. _(Discovery)_

## [0.9.0] - Build 10 - 2026-08-21

_Expired unused 2026-08-23. Contents shipped as Build 11._

### Fixed

- Series filter rails no longer lock the UI: `LibraryConsolidator` Series grouping is O(n) again (key-bucketed union). Documentary / multi-genre rails paint whole on first appearance. _(Discovery)_
- Apple TV Custom Rail editor: empty content axes hide after the catalog lands (match iOS); an empty picker gets a focusable Close instead of Menu exiting the app. Search-miss seats Close and does not yank focus back to the first row. _(Settings)_
- Series Continue Watching: episodes with no LastPlayedDate sink instead of winning the rail. _(Discovery)_
- Skip Intro prefers crowd windows over Emby typed / name-heuristic chapters; CrowdSkip remaps mega-season shows to absolute episode numbers. _(Playback)_
- AAC stream-copy lead-in A/V desync on dual-audio MKV (vendor #19 silence bridge). _(Playback)_
- Emby VOD black screen + audio on stub `avcC` (vendor #18). _(Playback)_
- Series detail synopsis + episode stills (TMDB aired-order remap for mega-seasons). _(Discovery)_
- Oblivion-class blank Emby movie backdrop (client image path, not server homework). _(Discovery)_
- In-progress web scrub / mark-as-watched now updates Continue Watching resume instead of a false checkmark. _(Discovery)_

### Changed

- Remove from Continue Watching keeps the title off the app rail (sticky hide). Emby web can still show it until HideFromResume — not this cut. _(Discovery)_

## [0.9.0] - Build 9 - 2026-07-31

### Added

- Clear Logo Source setting with Smart ranking (aspect gate, width-first in-band pick) and display-time transparent trim for padded logo canvases. _(Discovery)_
- Host `PlaybackEndProximityGate` for native end-of-file proximity (shared with software path). _(Playback)_

### Fixed

- Apple TV / iPhone: Aether resumes after app-switch or background (deferred arm so open-window resign does not race the first load). _(Playback)_
- Near-end demux `readError(-1)` on messy MKV tails: treat as EOF and let AVPlayer drain (no restart thrash); mid-title recovery give-up still soft-dismisses. Vendor patches #16 (preserve audio on reload) and #17. _(Playback)_
- Premature dismiss mid post-credits from early `didPlayToEndTime`. _(Playback)_
- Series detail focus returns to the last-played episode after binge advance + back. _(Discovery)_
- See-All Option A window slide: viewport stays put when new rows mount (residual focus-cursor stick parked). _(Library)_
- iOS portrait: hardware volume expands the in-chrome HUD when chrome is visible. _(Playback)_
- Dot-separated remux episode `Name` cleanup + TMDB title fallback when cleaned empty. _(Library)_
- Rewatch of an already-watched title still saves mid-title Resume below the auto-mark bar. _(Playback)_

### Changed

- iOS hardware volume sticky ~10% notches classified as OS `outputVolume` grid; no app snap. _(Playback)_

## [0.9.0] - Build 8 - 2026-07-25

### Fixed

- Apple TV Movies Favorites See-All load-more stalled after the first page when
  dual-version Emby favorites (UHD + HD) collapsed under LibraryConsolidator;
  Emby-paged Favorites now keep every favorited id (unconditional consolidate-skip),
  skip load-more while page-0 is in flight, and re-check data-end fetch when
  focus stays on the bottom row. _(Discovery)_
- Apple TV Movies Favorites See-All still stuck on page 0 after consolidator-skip
  alone: load-more no longer depends on focus reaching nearDataEnd on a 60-item
  mount window. Prefetch fills ~one Option A mount buffer on open;
  `FavoritesPaging.hasMore` keeps going on full pages; See-All refresh reloads
  FavoritesStore IDs. Series path mirrored. _(Discovery)_
- Apple TV Movies Favorites See-All stopped again after the second page: full-page
  `TotalRecordCount` equal to the loaded window no longer freezes `hasMore`, and
  Favorites keep a mount-sized tail buffer ahead of scroll progress so Option A
  focus does not have to sit on the absolute last row. Series mirrored.
  _(Discovery)_
- Apple TV Series/Movies Favorites See-All sibling versioning restored: display
  consolidates again (Demon Slayer / Doctor Who duplicate rows), while Emby
  paging advances on raw `StartIndex` / full-page receipt so load-more does not
  depend on consolidated grid growth. Tip stays build 8. _(Discovery)_

## [0.9.0] - Build 7 - 2026-07-24

### Added

- Player chrome consolidation on iPhone and Apple TV: Tracks / Navigate / More (chapters
  live under Navigate, not buried in gear). _(Playback)_
- Trakt layer-1: device OAuth + Keychain storage + DEBUG Connect (full history sync still
  upcoming). Honors Trakt `slow_down` with capped backoff while polling. _(Library)_
- Emby playlist create / reorder (iOS Reorder sheet; tvOS Add via focus-safe picker host).
  Device-confirm on large playlists still welcome. _(Library)_

### Fixed

- Text subtitles no longer sit mid-screen over the playback controls when chrome is up.
  _(Playback)_
- Skip Intro control cleared above the bottom chrome cluster after consolidation.
  _(Playback)_
- Host now consumes AetherEngine `liveSourceReset` and falls back to HLS AVPlayer when a
  live producer wedges (SSAI / no-cut stall class). Zap-fence so a disappearing player
  cannot start a late recovery. _(Live TV)_
- Live TV same-PID H.264 SPS / quality splice now rotates the fMP4 init so video does not
  freeze at the change (Annex-B detect → muxer `moov` rotation; Gate-0 verified). See From
  in-app reports. _(Live TV)_
- Apple TV rapid VOD scrub no longer stacks seek restarts into a buffering storm — chrome
  coalesces seeks while a prior seek is still landing. See From in-app reports. _(Playback)_
- Favorites See-All: first-paint parity, toast-only load-more, stable Emby page order
  (no scramble while paging). _(Discovery)_
- Emby See-All / library sort: UI order threaded into server pagination. _(Discovery)_
- Emby favorite hearts honor version siblings on See All, custom rails, and Search (toggling
  one encode updates the shared heart). _(Discovery)_
- Apple TV See-All scrubber stays on mounted posters (clamp at window edges; no blank-forever
  jump past the loaded set). _(Discovery)_
- See-All large grids: bounded poster window + focus stabilize on first window slide (Pass 2
  kept; true no-bounce polish parked Post-TF). _(Discovery)_
- Session logs flush on resign / background so a previous-session crash report still carries
  the lead-up. See From in-app reports. _(Settings)_

### Changed

- iOS player chrome edge insets retuned on device (horizontal inset 40). _(Playback)_
- Apple TV discovery hero fade / layout polish (portrait dimming, full-bleed under sidebar,
  breathing room to rails). _(Discovery)_
- Docs / screenshots refresh for FEATURES and README (public mirror). _(Docs)_
- Public tracking-issue close ritual documented (`docs/PUBLIC_ISSUE_CLOSE_RITUAL.md`).
  _(Docs)_

### From in-app reports

- [Previous-session logs missing after force-quit](https://github.com/peewee5/apotheosis-public/issues/28)
  — fixed by batched FileHandle sync + resign/background flush (device-confirmed; see also
  [#29](https://github.com/peewee5/apotheosis-public/issues/29)). _(Settings)_
- [Previous-session diagnostics restored after force-quit](https://github.com/peewee5/apotheosis-public/issues/29)
  — verification twin of the same durability fix (device-confirmed). _(Settings)_
- [Apple TV: rapid VOD scrub caused buffering stalls](https://github.com/peewee5/apotheosis-public/issues/27)
  — fixed by coalesce-while-landing scrub commits on tvOS player chrome (device-confirmed).
  _(Playback)_
- [Live TV: video freeze after mid-stream splice / quality change](https://github.com/peewee5/apotheosis-public/issues/22)
  — fixed by same-PID Annex-B SPS detect + fMP4 init rotation (synthetic Gate-0 verified;
  field soak still welcome). _(Live TV)_

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
