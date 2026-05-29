# Apotheosis: Feedback & Issue Tracker

**Apotheosis** is an iOS and tvOS media client for Emby, Xtream Codes (XC), and M3U/XMLTV playlists. One app for your self-hosted media server and your IPTV provider. See [`FEATURES.md`](FEATURES.md) for what's shipped, what's coming, and what's out of scope.

**Want in?** [Request beta access](https://forms.gle/aESrBZQWD4vZjuUA7). Invite-only TestFlight, round one is small.

This repo is the public face of Apotheosis for bug reports, feature requests, and beta feedback. The app's source lives in a private repo.

## What lives here

- **Issues:** Bugs filed through the in-app reporter land here automatically. You can also file one manually if something prevents the in-app reporter from working.
- **Discussions > Feature Requests:** Ideas, requests, "would be nice if". One thread per idea.
- **Discussions > Beta Feedback:** Per-round threads where current testers answer the survey and compare notes. See [`BETA_SURVEY.md`](BETA_SURVEY.md) for the current round's questions.
- **[`FEATURES.md`](FEATURES.md):** What the app does today, what's coming next, what's out of scope.

## Reporting a bug

**Easiest path: the in-app reporter.** Settings > Send Bug Report. It packages app version, iOS version, device model, and a redacted excerpt of the recent log buffer. Credentials, server URLs, and stream URLs are stripped before the payload leaves the device.

**Manual path:** [open an issue](../../issues/new). Include app version, iOS version, device model, what you did, what you expected, what happened.

## Filing a feature request

Open a thread in **Discussions > Feature Requests**. One idea per thread keeps the conversation focused. Search first to avoid duplicates.

## Beta surveys

If you're on the TestFlight beta, fill out the [current round's survey](https://forms.gle/9N1M99NinnUG57yS8). The full question list is in [`BETA_SURVEY.md`](BETA_SURVEY.md) if you want to read through before filling it out.

## Privacy

The in-app reporter is the only thing that leaves your device automatically, and it's scrubbed before transmission (no credentials, no server URLs, no stream URLs). There's no analytics SDK in the app. The bug pipeline goes through a Cloudflare Worker that creates the GitHub Issue server-side, so the GitHub token never ships in the app binary.

Full security spec for the curious: it lives with the app source. Ask if you want details.
