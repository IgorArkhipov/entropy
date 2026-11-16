# Real Phenom USB checks, 2026-11-16

These are captures of an actual connected keyboard in unmodified Entropy PR builds. They are separate from the simulated UI previews in the parent directory.

- Host: macOS 27.2, build 26B123, native Apple Silicon.
- Device: Ergohaven Phenom over USB, VID:PID `E126:0052`.
- Runtime firmware: `4.0.5`, VIA protocol 9 / Vial protocol 6.
- Both builds loaded the real 16-layer layout. A complete local `.entlayout` backup was exported through the running application's IPC. The user's layout is not published here.
- No firmware reset, flashing, layout import or configuration edit was performed.

## PR #275

Source: `3b5fae8b4020d7058c8d057e6b42930856bb1934`.

`pr275-phenom-vial-about.png` shows the actual firmware and the product's eligibility message: in-app flashing requires RMK 0.3+ with Rynk over USB. The currently connected keyboard runs QMK/Vial, so this setup does not yet provide the requested guided-update evidence. The reviewer requirement remains pending.

The published RMK release list was also checked: `v0.3.0` is the only stable release containing Phenom packages; earlier releases contain none. The current guide requires a stable installed version >= 0.3.0 and `UpdateAvailable`, so manually migrating to 0.3.0 would still not provide an eligible published upgrade. A newer supported release or an explicitly designed same-version reinstall path is needed to exercise the complete guide. No version spoofing or synthetic release metadata was used.

## PR #277

Source: `c79664fae18777e404ce06c244b8c52f10cef5b4`.

The initial update lookup returned HTTP 403. `pr277-github-rate-limit.png` captures the exact endpoint and status. A separate unauthenticated request confirmed `x-ratelimit-remaining: 0` and reset time 2026-11-16 10:48:01 PST. Authenticated release metadata confirms the expected QMK asset is `4.2.0_phenom_v1.uf2`, 198144 bytes, SHA-256 `5ae097a1fb9f85822ee022de8101cf1c9ff4f1dddf8e0334f59979e283ffbcca`.

After the rate-limit reset, the real application lookup succeeded:

1. Opened Layout -> About device in the unmodified PR #277 build with the real Phenom connected.
2. Pressed Check. Entropy reported current firmware `4.0.5`, latest firmware `4.2.0`, update available, and package `4.2.0_phenom_v1.uf2`. See `pr277-phenom-selected-package.png`.
3. Pressed Entropy's Download button. The system browser downloaded the selected published firmware into Downloads. That exact filename was absent before this test.
4. Verified the resulting file: 198144 bytes, SHA-256 `5ae097a1fb9f85822ee022de8101cf1c9ff4f1dddf8e0334f59979e283ffbcca`, matching GitHub's published release-asset digest. The file modification time was 2026-11-16 10:49:06 PST. See `download-result.json`.

This is an actual successful in-app lookup and browser-mediated download. No firmware was installed.

The original RMK 0.3 model-only ZIP regression cannot be reproduced physically with the currently installed QMK/Vial firmware. Any successful QMK download is a hardware compatibility check for that firmware family, not physical proof of the RMK ZIP fix.
