# Apotheosis: Feedback & Issue Tracker

This repo is the public face of [Apotheosis](TestFlight link coming) for bug reports, feature requests, and beta feedback. The app's source lives in a private repo.

## What lives here

- **Issues** — Bugs filed through the in-app reporter land here automatically. You can also file one manually if something prevents the in-app reporter from working.
- **Discussions → Feature Requests** — Ideas, requests, "would be nice if". One thread per idea.
- **Discussions → Beta Feedback** — Per-round threads where current testers answer the survey and compare notes. See [`BETA_SURVEY.md`](BETA_SURVEY.md) for the current round's questions.
- **[`FEATURES.md`](FEATURES.md)** — What the app does today, what's coming next, what's out of scope.

## Reporting a bug

**Easiest path: the in-app reporter.** Settings → Send Bug Report. It packages app version, iOS version, device model, and a redacted excerpt of the recent log buffer. Credentials, server URLs, and stream URLs are stripped before the payload leaves the device.

**Manual path:** [open an issue](../../issues/new). Include app version, iOS version, device model, what you did, what you expected, what happened.

## Filing a feature request

Open a thread in **Discussions → Feature Requests**. One idea per thread keeps the conversation focused. Search first to avoid duplicates.

## Beta surveys

If you're on the TestFlight beta, the current round's survey is in [`BETA_SURVEY.md`](BETA_SURVEY.md). Answers go in the matching Discussions thread under "Beta Feedback". Threaded responses let us follow up on specific points without losing the rest of your feedback.

## Privacy

The in-app reporter is the only thing that leaves your device automatically, and it's scrubbed before transmission (no credentials, no server URLs, no stream URLs). There's no analytics SDK in the app. The bug pipeline goes through a Cloudflare Worker that creates the GitHub Issue server-side, so the GitHub token never ships in the app binary.

Full security spec for the curious: it lives with the app source. Ask if you want details.
