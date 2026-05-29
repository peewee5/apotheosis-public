# Beta Survey

**Fill it out here:** [Google Form](https://forms.gle/9N1M99NinnUG57yS8). Takes 5-10 minutes. Answer whatever resonates.

The questions are written out below if you'd rather skim them first before deciding what to fill in.

---

If you're on the TestFlight beta, these are the questions we want answers to for the current round. Post any extra notes or follow-ups in the matching thread under **Discussions → Beta Feedback**.

Skip any question that doesn't apply. Partial answers are fine. Honest "this felt weird" is more useful than diplomatic "this was fine".

---

## UX feel

No right answers here. We want preference data.

1. **Tab bar tooltip.** When you slide across tabs, the label tooltip appears for ~1.5 seconds. Too long once you know the icons? Too short the first time you saw them?
2. **Watched item dimming.** Watched posters dim to 50% opacity on the rails. Does that feel right, or is it too aggressive (closer to 65% would be a gentler nudge)?
3. **Auto-mark watched.** Currently fires at 95% of runtime. Right threshold, or should it bail at 90% (catches people who quit before the last scene) or 98% (only marks truly finished)?
4. **Swipe down to minimise the player.** Does the gesture feel intentional, or do you accidentally trigger it? Especially curious about different grip styles.
5. **Mini player gestures.** Swipe up expands the mini bar, swipe down dismisses it. Discoverable without a hint, or did you only learn this by accident?
6. **Source indicator.** Each item shows a source tag (Emby, XC, M3U). Two designs in play: a coloured dot vs. a glowing text monogram (E, XC, M3U). Which feels more natural in the chip row? The dot is subtle and learns with use; the monogram is immediately readable but has more visual weight.
7. **Source dot colour map** (if dots are kept). Emby=green, XC=white, M3U=aqua. Do you learn the mapping quickly? Particularly: do XC (white) and M3U (aqua) feel distinguishable for dual-source users?
8. **Source visibility and tabs.** If you hide a source in Settings → Source Visibility, would you expect the tab for that source to disappear too? Or keep tabs as a separate decision? Currently they're independent.
9. **EPG time density.** The EPG grid shows about 30 minutes per screen in portrait and an hour in landscape. Too compressed, about right, or would you prefer less time visible at once with more detail per slot?
10. **Continue Watching with re-watches.** If you mark something watched and then start it again, it shows up in Continue Watching until you finish or remove it manually. Expected, or would you prefer CW only surfaces things you haven't finished?
11. **Settings findability.** Is there anything in Settings you had trouble finding, or expected to be somewhere different?
12. **One sentence.** If you were describing this app to someone who hasn't heard of it, how would you put it in one sentence?

---

## Specific scenarios to try

These are the paths most likely to surface bugs.

1. **Custom rails.** Create a rail with two or three filter axes (genre + decade + source, for example). Does the "See All" destination show what you expected?
2. **Language filter.** Create a language-filtered rail (Japanese is a good test if you have anime). Does it correctly surface content where Japanese is the primary audio?
3. **Large library pagination.** If you have a library with more than 1000 items, do the items beyond the first 1000 appear after a few seconds of scrolling?
4. **AirPlay with VLC content.** Start an MKV from Emby, then activate AirPlay. Expect a brief pause then handoff to AVPlayer on the receiver. Disconnect AirPlay. Expect to swap back to local VLC playback at the same position.
5. **AirPlay with live TV.** Activate AirPlay on an XC live stream. Does it route cleanly?
6. **Picture-in-Picture for VOD.** Start a movie or episode, swipe away to background or hit the PiP button. Does PiP engage cleanly for both Emby and XC content?
7. **iCloud sync.** Watch something on one device (signed into iCloud), open Apotheosis on a second device on the same Apple ID. Does watch state and resume position carry over?
8. **VLC engine content.** If you played any MKV, AVI, or FLV files, Apotheosis routes these through a different engine (VLC) automatically. Did the player feel comparable to native content? Any differences in controls, title display, or quality?
9. **Track language persistence.** Set a preferred audio language in Settings → Audio & Subtitles. Play episode 1 of a series, then skip to episode 2. Did the language carry over?

---

## Player chrome on real hardware

A few interactions only reproduce on a real device. If you can:

1. **Gear menu double-tap.** Does the gear submenu need a double-tap to open during initial playback, or does single-tap work?
2. **Mute icon linger.** After muting via the gear menu, does the gear icon stay visible after the chrome auto-hides?
3. **Volume drag.** Drag the volume slider in the player. Does it apply in real time, or only on release?
4. **System volume gesture.** Drag down the left side of the player. Does it actually change your iPhone's system volume (you'll hear the system volume HUD), or does it only attenuate the in-player audio?
5. **PiP auto-trigger.** When you press Home while something is playing via AVPlayer, Picture in Picture activates automatically. Does that feel right, or would you rather the player just paused?

---

## Accessibility

1. **Colour blindness.** Apotheosis uses a colour map for source indicators tuned for deuteranopia/protanomaly (Wong 2011 palette). If you have any form of colour vision difference, do the source colours read distinctly for you? Specifically Emby (green), XC (white), M3U (aqua).

---

## Anything else

Stuff that doesn't fit a category, or that we didn't think to ask about. The best feedback is usually the "this felt off but I can't articulate why" stuff. Put it here and we'll follow up.
