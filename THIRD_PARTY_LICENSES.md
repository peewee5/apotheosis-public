# Open Source Licenses

Apotheosis is built on a lot of open source work. This document lists every third-party library that ships inside the app, the license each one is distributed under, its copyright holders, and where to get its source. The full verbatim text of every license referenced here is in the companion file `ThirdPartyLicenseTexts.txt`, which is bundled inside the app and viewable from Settings.

If you spot something inaccurate or missing, please open an issue. Getting attribution right matters.

## How the player engine is built

Apotheosis plays video on **iPhone, iPad, and Apple TV** through a single engine: **AetherEngine**, which builds on the **FFmpeg** libraries (demux plus stream-copy remux) and hands decoding to Apple's VideoToolbox and AVFoundation. AetherEngine is distributed under the LGPL v3.0 with an additional App Store distribution permission; FFmpeg is distributed under the LGPL v2.1.

The FFmpeg build is the **non-GPL** configuration: it is built with no `--enable-gpl` and no `--enable-nonfree`, so no GPL-only or nonfree components are linked in. AetherEngine links only its core product (the optional SMB component, whose dependency carries no App Store exception, is **not** included). Everything in the inventory below is either LGPL or a permissive license, so the app stays distributable under the LGPL terms.

## Source code availability and the LGPL written offer

The libraries below that are covered by the LGPL are linked statically. Under the LGPL (v2.1 section 6 and v3.0 section 4), anyone who receives the app is entitled to the means to relink it against a modified version of those libraries.

To honor that:

1. **Library source.** The complete corresponding source for every LGPL component is available from the upstream project at the version Apotheosis ships. The upstream link for each one is in the table below. The exact pinned versions are recorded in the app's `Package.resolved` (FFmpegBuild 1.0.1, LibDovi 1.0.2, AetherEngine vendored from upstream 3.13.2), and the FFmpegBuild release artifacts mirror the binaries built from that FFmpeg source.

2. **Relinkable application.** On request, the author will provide the Apotheosis application object code in a form that lets you relink it against a modified version of any LGPL library it uses (or otherwise satisfy the applicable LGPL relink clause). Email **apotheosis@aomosk.com** with the app version you have. This offer is valid for as long as the LGPL requires for the version you received, and it is also published here on the public repository.

No charge, no catch. The point of the LGPL is that you can swap in your own build of these libraries, and that should stay true even though Apotheosis is a closed-source app.

## Inventory

Versions are given where they are pinned and confirmed. For FFmpeg there is no single project-wide copyright line (the copyright is per file, held by the many contributors), so it is attributed to its developers and contributors, which is how the project asks to be credited.

### Media engine (iPhone, iPad, and Apple TV)

| Component | License | Copyright | Source |
|---|---|---|---|
| AetherEngine (vendored from upstream 3.13.2) | LGPL-3.0-or-later (with App Store / DRM exception) | Copyright (C) 2026 Vincent Herbst | https://github.com/superuser404notfound/AetherEngine |
| FFmpeg (libavcodec, libavformat, libavutil, libavfilter, libswscale, libswresample) | LGPL-2.1-or-later (non-GPL build) | The FFmpeg developers and contributors | https://ffmpeg.org |
| FFmpegBuild 1.0.1 (prebuilt FFmpeg xcframeworks) | LGPL-3.0-or-later | The FFmpegBuild authors | https://github.com/superuser404notfound/FFmpegBuild |
| libdovi / dovi_tool (LibDovi 1.0.2) | MIT | Copyright (c) quietvoid | https://github.com/quietvoid/dovi_tool |
| dav1d 1.5.1 (AV1 decoder, linked via FFmpegBuild) | BSD-2-Clause | Copyright (c) 2018-2019, VideoLAN and dav1d authors. All rights reserved. | https://code.videolan.org/videolan/dav1d |
| zimg 3.0.5 (zscale colorspace / scaling backend, linked via FFmpegBuild) | WTFPL Version 2 (imposes no conditions; courtesy credit) | Copyright (c) the zimg contributors | https://github.com/sekrit-twc/zimg |

## License texts

The complete text of each license named above (LGPL v2.1, LGPL v3.0, and GPL v3.0 as the base of the LGPL v3.0, MIT, and BSD-2-Clause for dav1d), together with AetherEngine's App Store / DRM exception, is in `ThirdPartyLicenseTexts.txt`. That file ships inside the app, so the licenses travel with every copy. zimg is under the WTFPL Version 2, a public-domain-equivalent license that imposes no conditions (no attribution or notice reproduction required); it is credited here as a courtesy and its canonical text is at http://www.wtfpl.net/txt/copying/.
