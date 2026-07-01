# Security Policy

Apotheosis is a client for media servers you control or subscribe to. It holds credentials for those servers and sends your data nowhere else. That framing shapes what matters here: this is a credential-bearing client, not a service with a backend of its own.

## Supported versions

Fixes land on the current build. Older builds are not back-patched, so picking up a fix means updating to the latest TestFlight or App Store release.

| Version | Supported |
| ------- | ---------- |
| Latest TestFlight / App Store build | :white_check_mark: |
| Anything older | :x: |

## Reporting a vulnerability

Please report security issues **privately**, not as a public issue or pull request. Two ways, whichever you prefer:

- **GitHub private advisory** (preferred): [Security -> Report a vulnerability](https://github.com/peewee5/apotheosis-public/security/advisories/new). It stays visible only to you and the maintainer.
- **Email**: apotheosis@aomosk.com.

Please do not put real server URLs, credentials, tokens, or stream URLs in a report. If you need to show a request or a log line, redact the host and any auth first. A redacted proof of concept is plenty.

Helpful to include:

- The app version and platform (iOS / iPadOS / tvOS).
- A description of the issue and its impact.
- Steps or a proof of concept that reproduce it. For a malformed-media crash, a sample file or `ffprobe` output is ideal.

Expect an acknowledgement within a few days. When a fix ships, the advisory is published with credit unless you would rather stay anonymous.

## Scope

Apotheosis connects to media servers (Emby, Jellyfin, Plex, Xtream Codes IPTV, M3U/XMLTV) that the developer does not operate, and it parses untrusted media and playlist data. The areas most relevant to security:

- **Credential handling.** Server credentials and tokens live in the iOS Keychain, this-device-only by default. They are never written to plain storage and never leave the device except to the server they belong to. iCloud Keychain sync is off unless you explicitly turn it on.
- **Network transport.** How the app talks to your servers, including TLS trust decisions for self-signed servers on a home network and the redirect handling for IPTV stream CDNs.
- **Media parsing.** Demuxing and decoding of untrusted containers, subtitles, and playlists (the FFmpeg and dav1d surface inside the playback engine, plus the M3U and XMLTV parsers).
- **Diagnostics.** The in-app bug reporter redacts server URLs, hosts, credentials, and stream URLs on the device before anything is sent. Reports carry no analytics and no tracking identifiers.

Out of scope here: vulnerabilities in the media servers themselves (Emby, Jellyfin, Plex, or an IPTV provider's panel) belong on their own trackers, and issues in upstream FFmpeg or dav1d should go upstream, though we are glad to know if a bundled build is affected.

## What Apotheosis does not do

- No analytics, no tracking, no third-party telemetry SDKs.
- No advertising identifiers.
- No account of its own, and no server that ever sees your library or your credentials.
