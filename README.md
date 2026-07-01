# Apotheosis

Most IPTV clients pretend your personal media library doesn't exist. Most media players don't know what IPTV is. Apotheosis handles both.

<p>
  <img src="https://img.shields.io/badge/platforms-iOS%20%7C%20iPadOS%20%7C%20tvOS-informational" alt="platforms">
  <img src="https://img.shields.io/badge/TestFlight-invite--only-blue" alt="TestFlight, invite only">
  <img src="https://img.shields.io/badge/telemetry-none-brightgreen" alt="no telemetry">
</p>

![Apotheosis on Apple TV](docs/screenshots/tvos-discovery-hero.png)

One client for **iPhone, iPad, and Apple TV** that treats **Emby**, **Jellyfin**, **Xtream Codes IPTV**, and **M3U/XMLTV** as equals: curated discovery, a direct-play player that doesn't transcode your files, and Live TV with a real EPG grid. No backend of its own. Your servers, your data.

> **In TestFlight, invite-only.** [Request access](https://forms.gle/aESrBZQWD4vZjuUA7) or [file a bug](#bugs--feature-requests). Current rough edges are under [Known issues](#known-issues).

---

## Screenshots

Apple TV and iPhone, the same app.

<table>
  <tr>
    <td width="50%"><img src="docs/screenshots/tvos-player-chrome.png" alt="Player on Apple TV"></td>
    <td width="50%"><img src="docs/screenshots/tvos-epg-grid.png" alt="Live TV guide on Apple TV"></td>
  </tr>
  <tr>
    <td width="50%"><img src="docs/screenshots/player-chrome-full.png" alt="Player on iPhone"></td>
    <td width="50%"><img src="docs/screenshots/continue-watching-hero.png" alt="Continue Watching on iPhone"></td>
  </tr>
</table>

More, annotated, in [`FEATURES.md`](FEATURES.md), including the version-sibling dedup shown side by side against Infuse.

---

## Why it exists

There's a gap nothing fills well. Infuse is the best personal media client available, but it barely tolerates IPTV. Pure IPTV apps (TiviMate, IPTV Smarters) don't know Emby exists. Run both and you're either switching apps constantly or living with a client that does one thing well and the other badly.

Apotheosis treats your library and your IPTV as first-class peers. Continue Watching works across both. Favorites sync across both. One player, one library, one tab bar, on the phone in your pocket and the TV on your wall.

---

## Sources

**Emby**: direct login and Emby Connect. Full library browsing, Continue Watching with resume, two-way Favorites sync, playback reporting, and version chips for multi-encode libraries (1080p and 4K show as one poster with resolution chips, not two entries).

**Jellyfin** (early support): add a server from the same screen as Emby. The app detects which one you're connecting to and reuses the Emby path, so browsing, Continue Watching, and playback work the same way. Still being road-tested.

**Xtream Codes (XC) IPTV**: VOD, Series, and Live TV. Account expiry and connection status in Settings. Favorites synced to iCloud so they survive reinstalls.

**M3U + XMLTV**: paste a playlist URL. Handles 70k+ channel playlists with CRLF line endings, file-backed storage to get past the UserDefaults 4 MB cap, and XMLTV EPG matched by tvg-id.

Plex is on the roadmap.

---

## Player

One direct-play engine across iPhone, iPad, and Apple TV. It demuxes with FFmpeg and hands decoding to Apple's VideoToolbox, so 4K HDR, HEVC 10-bit, MKV, and raw MPEG-TS play with no transcoding and no server re-encode. AVPlayer handles HLS and AirPlay and stands in as a fallback.

That matters most on Apple TV, where AVPlayer on its own can't reliably play those formats. The chrome, skip markers, auto-play-next, and in-player episode picker are the same on all three platforms.

Volume control writes to the actual system volume (the hardware buttons move the on-screen HUD in real time). A brightness drag adjusts the screen without leaving the player. Both work on live and VOD.

Skip Intro and Skip Credits surface on their own when the playhead enters a marked region, even with the chrome hidden, so the anime cold-open case doesn't make you tap to reveal the controls first. Markers come from the server where it exposes them.

The mini player keeps playback alive while you browse, and a compact dock mode collapses it to a single pill when you scroll so the tab bar and the player controls stop fighting for room. On iPhone and iPad, Picture in Picture hands off to the system and can drop the app to the home screen, Infuse-style.

---

## Live TV

An EPG grid with a sticky channel column, horizontal time scroll, and a now-line that tracks the centre. XMLTV and XC EPG both fill it, with a little jitter on the opening fetch burst so an XC server doesn't rate-limit you out of the gate.

Categories past ~1,500 channels swap the grid for a searchable list, so a 30k-channel reseller dump stays smooth instead of choking. Drop back to a normal-sized category and the guide comes back on its own.

Quick Chips above the category menu pin channels or categories for one-tap access. In the player, prev/next channel buttons replace the seek controls on a live stream, and navigation stays in place with no dismiss animation.

---

## Discovery

Continue Watching surfaces the most recent item across every connected source. Version siblings (1080p/4K) share one tile instead of doubling up, and Mark as Watched clears the tile right away without waiting on the server.

Custom Rails compose filter rails from a dozen axes: genre, decade, source, person (autocomplete against cast data), rating floor, resolution, watched state, recency, studio, audio language, and curated source (Emby BoxSets or Playlists). Each renders above the source's own rails.

See All views paginate as you scroll, 100 at a time with no artificial cap, so a 30k-item library loads without freezing.

---

## Privacy & Security

Apotheosis holds credentials for servers you control, and it treats them like it. They live in the iOS Keychain, this-device-only by default, and never leave the device except to the server they belong to. There is no analytics, no tracking SDK, and no telemetry of any kind. In-app bug reports redact server URLs, hosts, credentials, and stream URLs on the device before anything is sent.

Full policy, scope, and how to report a vulnerability privately: [`SECURITY.md`](SECURITY.md).

---

## Known issues

Being actively worked on:

- **Apple TV: the player doesn't resume after an app switch.** Background the player through the app switcher, come back, and playback won't pick up. Back out and reopen for now. Fix identified.
- **Rare glitching on some broadcast-sourced files.** A small class of non-standard encodes (typically DVR or broadcast captures) can artifact. Diagnosed, fix planned.
- **Live TV can take a few seconds to settle** at startup, occasionally with brief audio/video sync drift that corrects itself.
- **Some live streams stall on first play** now and then (a provider-side network quirk); the player auto-retries and usually recovers.
- **iPad uses the iPhone layout** for now. Its own pass is coming.
- **Subtitles can take a moment to appear** the first time you turn them on for a large remote file.

---

## Bugs + Feature Requests

File issues here on [apotheosis-public](https://github.com/peewee5/apotheosis-public), or send one from the app (Settings > Bug Report / Feature Request). In-app reports attach a filtered log excerpt, and if the app restarted unexpectedly they carry the previous session's log too, so the lead-up to a crash isn't lost.

Don't paste server URLs, credentials, or stream URLs into a report. The in-app reporter redacts them; the GitHub form does not.

---

## Under the hood

Apotheosis is a closed-source app, but here's the shape of it. SwiftUI throughout, `@Observable` view models, iOS 18+ and tvOS 18+. A single `ItemKey` gives every title a stable identity across sources (`emby:serverKey:itemId`, `xc:live:-N`) that threads through resume, favorites, track preferences, and in-player navigation, which is what lets Continue Watching and Favorites work as one list instead of four. Playback runs on a vendored engine (AetherEngine: FFmpeg demux plus a VideoToolbox decode path) behind engine-agnostic controls, so the chrome doesn't care what's decoding underneath.

---

## Built with

Apotheosis is designed, built, and shipped by [peewee5](https://github.com/peewee5) in close pair-programming with **Claude** (Anthropic). The commit log is the receipt: nearly every commit carries a `Co-Authored-By: Claude` trailer.

Playback runs on **[AetherEngine](https://github.com/superuser404notfound/AetherEngine)** (FFmpeg demux plus a VideoToolbox decode path), which does the direct-play heavy lifting. Thanks also to **[Moonfin](https://github.com/Moonfin-Client/Moonfin-Core)**, an early reference for what a great custom player on tvOS can be.

## License

Apotheosis is closed-source. It builds on open-source components (AetherEngine, FFmpeg, dav1d, and others) under the LGPL and permissive licenses, with no GPL or nonfree parts. The full inventory, the license texts, and the LGPL relink offer are in [`THIRD_PARTY_LICENSES.md`](THIRD_PARTY_LICENSES.md).
