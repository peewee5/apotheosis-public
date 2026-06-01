# Apotheosis

Most IPTV clients pretend your personal media library doesn't exist. Most media players don't know what IPTV is. Apotheosis handles both.

One iOS and tvOS client for **Emby**, **Xtream Codes IPTV**, and **M3U/XMLTV**. Curated discovery, a full custom player, and Live TV with a proper EPG grid. No backend of its own. Your servers, your data.

> **In TestFlight now, invite-only.** Round one is small and going out to trusted testers. [Request access](https://forms.gle/aESrBZQWD4vZjuUA7) or [file a bug](#bugs--feature-requests).

---

## What it looks like

See [`FEATURES.md`](FEATURES.md) for annotated screenshots: discovery, the EPG grid, the player chrome, and the version-sibling dedup shown side by side against Infuse.

---

## Why it exists

There's a gap in the market that nothing fills well. Infuse is the best personal media client available, but it barely tolerates IPTV. Pure IPTV apps (TiviMate, IPTV Smarters) don't know Emby exists. If you run both, you're either switching apps constantly or settling for a client that does one thing well and the other badly.

Apotheosis treats Emby and XC IPTV as first-class peers. Continue Watching works across both. Favorites sync across both. One player, one library, one tab bar.

---

## Sources

**Emby**: direct login and Emby Connect. Full library browsing, Continue Watching with resume position, two-way Favorites sync, playback reporting, version chips for multi-encode libraries (1080p and 4K show as one poster with resolution chips, not two entries).

**Xtream Codes (XC) IPTV**: VOD, Series, and Live TV. Account expiry and connection status in Settings. Favorites synced to iCloud so they survive reinstalls.

**M3U + XMLTV**: paste a playlist URL. Handles 70k+ channel playlists with CRLF line endings, file-backed storage to bypass the UserDefaults 4 MB cap, XMLTV EPG matched by tvg-id.

---

## Player

Dual-engine: AVPlayer for HLS and native Apple formats, MobileVLCKit for MKV, AVI, FLV, raw MPEG-TS, and anything AVPlayer won't touch. If AVPlayer fails to start, it falls back to VLC automatically.

Volume control writes to actual system volume (hardware buttons update the on-screen HUD in real time). Brightness drag adjusts screen brightness without leaving the player. Both work on live and VOD.

Skip Intro and Skip Credits auto-surface when the playhead enters a marked region, even if the chrome is hidden. Great for the anime cold-open case where you'd otherwise have to tap to surface the chrome first. Today the markers come from Emby chapters named "Intro" or "Outro" (typically populated by the Chapter Markers plugin) or from hand-curated entries. Native Emby Premiere intro detection and Jellyfin's Intro Skipper plugin endpoint are on the roadmap.

Mini player keeps the engine alive while you browse. Compact dock mode collapses everything to a single pill when you scroll down so the tab bar and player controls don't fight for space.

---

## Live TV

EPG grid with sticky channel column, horizontal time scroll, and a current-time indicator that tracks the centre. XMLTV and XC EPG both populate it. 800ms jitter on individual EPG fetches prevents rate-limiting on the initial burst against XC servers.

Categories past ~1,500 channels swap the grid for a searchable list or card browser, so a 30k-channel reseller dump stays smooth and searchable instead of choking. Drop back to a normal-sized category and the guide returns on its own.

Quick Chips above the category menu: pin channels or categories for one-tap access. Prev/next channel buttons in-player replace the seek controls on live streams. Navigation is in-place with no dismiss animation.

---

## Discovery

Continue Watching surfaces the most recently played item for both Emby and XC VOD. Emby items store under canonical and direct keys so version siblings (1080p/4K) share the same CW tile correctly. Mark as Watched clears the tile immediately without waiting for a server round trip.

Custom Rails let you compose filter rails from 11 axes: genre, decade, source, person (autocomplete against Emby's cast data), rating floor, resolution, watched state, recency, studio, audio language, and curated source (Emby BoxSets or Playlists). Up to several rails per tab, each rendered above the source-primary rails.

See All views paginate incrementally: first 100 items on load, next 100 triggered as you scroll near the end. No artificial cap, so 30k-item libraries load without freezing.

---

## Platform details

- iOS 18+ and tvOS 18+. SwiftUI throughout. `@Observable` viewmodels, no `ObservableObject`.
- XcodeGen: `project.yml` is the source of truth, `.xcodeproj` is gitignored.
- MobileVLCKit via Swift Package Manager.
- Privacy manifest declares `NSPrivacyTracking: false`. No analytics, no tracking SDK, no third-party telemetry. In-app bug reports go through a Cloudflare Worker that creates GitHub Issues; the GitHub token never ships in the binary.

---

## Bugs + Feature Requests

File issues and feature requests at [apotheosis-public](https://github.com/peewee5/apotheosis-public), or submit directly from the app (Settings > Bug Report / Feature Request). In-app reports attach a filtered log excerpt automatically, and if the app restarted unexpectedly they carry the previous session's log too, so the lead-up to a crash isn't lost.

Don't paste server URLs, credentials, or stream URLs into bug reports. The in-app reporter redacts them; the GitHub form doesn't.

---

## Build from source

You'll need Xcode 16+, [XcodeGen](https://github.com/yonaskolb/XcodeGen), and an Apple Developer account for on-device builds. Simulator works without one.

```sh
brew install xcodegen
git clone <repo>
cd media
xcodegen generate
open Apotheosis.xcodeproj
```

Pick `Apotheosis-iOS` or `Apotheosis-tvOS` and run. Re-run `xcodegen generate` after pulling if new Swift files were added.

```sh
# CLI build (iOS Simulator)
xcodebuild -scheme Apotheosis-iOS \
  -destination 'platform=iOS Simulator,name=iPhone 17 Pro' \
  build
```

---

## Architecture (brief)

```
App/            entry point, tab bar, player wiring
Features/       Movies, Series, LiveTV, Playback, Settings
Sources/        Emby, XC, M3U clients and models
Core/           models, networking, storage, logger
Theme/          shared UI components
```

Key patterns: `ItemKey` gives stable cross-source identity (`emby:serverKey:itemId`, `xc:live:-N`) that threads through resume, favorites, track preferences, and in-player navigation. `PlayerControls` is engine-agnostic state shared by AVPlayer and VLC chrome so the UI doesn't care which engine is active.

---

## Known limitations

- tvOS compiles and plays, but the interaction layer is built for touch, so it's a port rather than a layout tweak. Post-beta work. iPad layout is iPhone-tuned for now and gets its pass sooner.
- System volume control uses a grey-area MPVolumeView path. If Apple closes it in a future iOS update, the chrome falls back to per-player gain automatically.
- Plex and Jellyfin are on the post-v1 roadmap. Not in beta.
