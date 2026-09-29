# GeoClock Offline for Windows

A community-maintained portable Windows x64 app based on
[jpettitt/geo-clock-card](https://github.com/jpettitt/geo-clock-card).
The clock, map images, timezone data, and meeting planner are bundled for offline use.
Locations are entered manually with coordinates.

## Download and run

1. Open the [Windows v0.1.1 release](https://github.com/mr0ng/geo-clock-card/releases/tag/windows-v0.1.1)
   and download `GeoClock-Offline-0.1.1-win-x64.exe`.
2. Double-click the EXE. No installation of Node, Git, Python, WebView2, or a browser
   is needed to run the app.

This is an unsigned prerelease; Windows may display a publisher warning.
The release includes `SHA256SUMS.txt`. See the [verification record](desktop/VERIFICATION.md)
for the published size, checksum, checks performed, and remaining limits.

Use **Customize** to add locations. **F11** toggles fullscreen; **Escape** or the
exit icon returns to the normal window. The app saves settings locally unless
**Remember settings** is turned off.

## Help and project ownership

- Windows app, packaging, or download problems: [open an issue on this fork](https://github.com/mr0ng/geo-clock-card/issues).
- Shared clock/card problems: [upstream project and issues](https://github.com/jpettitt/geo-clock-card).
- Website and browser use: [geoclock.world](https://geoclock.world).
- Mac app: [upstream macOS companion](https://github.com/jpettitt/geoclock-wallpaper-mac).

This fork owns the Windows wrapper and its releases. The original project owns
the shared clock, website, and other platform integrations.

## Build and maintain

See [desktop/README.md](desktop/README.md) for build instructions and runtime details.
The fork's `main` follows upstream; `codex/windows-offline-app` is the default branch
for Windows development. Upstream updates are reviewed and merged into that branch.

The original GeoClock Card code and its copyright notices are retained under the
[MIT license](LICENSE). Bundled imagery and data credits are available in the app's About page.
