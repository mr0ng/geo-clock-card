# Local verification record

Build verified: 2026-09-27. Release record corrected: 2026-09-28.
This record describes the published `windows-v0.1.1` build from source commit
`793b8c76727d6b2364ee597791dfb61cb75436ad`. Later documentation and line-ending
changes on `codex/windows-offline-app` do not change that published build.

## Build

- Upstream base: `c4870ee172042fe7317fbee52fae299dee84164c`, card version 0.3.0.
- Desktop version: 0.1.1; the build includes local changes on that base.
- Builder host: Windows 10 x64, OS build 19045; Node 24.19.0, npm 11.17.0.
- Pinned development dependencies: Electron 44.4.5, electron-builder 26.15.3.
- Packaged runtime: Electron 44.4.5, Chromium 152.0.7977.130, Node 24.21.0.
- Published assets: `GeoClock-Offline-0.1.1-win-x64.exe` and `SHA256SUMS.txt` in
  [Windows v0.1.1](https://github.com/mr0ng/geo-clock-card/releases/tag/windows-v0.1.1).
- The published rebuild was generated under `desktop/release/candidate/`,
  with `win-unpacked/` alongside the EXE. Build output is excluded from Git.
- Signing: unsigned; default Electron icon. No signing identity or personal
  publisher information was used.
- Published portable EXE: 112,315,114 bytes (107.1 MiB).
- SHA-256: `bd119f53de3f6803e12ae8ae0a80bf00fb79be14f148b35f55ac8b96d941c727`.
- The EXE size and SHA-256 match GitHub's release asset metadata, the published
  `SHA256SUMS.txt`, and the locally retained EXE. An earlier draft candidate was
  rebuilt after the Remember and About fixes; its size had been left in this
  record by mistake. This correction leaves the published tag and EXE intact.

## Passing checks

| Check | Result |
| --- | --- |
| Node unit checks | 6 passed: protocol allowlist, request methods, traversal/encoding rejection, outbound policy, corrupt/offscreen window bounds, complete asset assembly and missing-source failure. |
| Assembly | 36 local files, including all 28 clock assets: 24 seasonal day images, one night image, two timezone datasets and the prebuilt clock bundle. Sizes and SHA-256 hashes verified. |
| Electron smoke | Actual sandboxed renderer loaded from `geoclock://app`, with context isolation enabled and Node integration disabled. |
| Outbound requests | External HTTPS session request rejected; session and renderer requests to a controlled HTTP server rejected, with zero server hits. Location permission denied and new windows blocked. |
| Offline UI | Manual coordinate inputs available; online search, live location and share controls absent. Invalid latitude rejected; zero coordinates accepted. Add, rename and remove exercised. |
| Persistence | Locations survived reload and graceful window close/reopen. Planner working hours persisted. Turning Remember off cleared both clock and planner saved settings, stayed off after reopening, and kept later edits unsaved. Turning it back on resumed persistence across a further reopen. |
| About and license | The MIT license is shown inside About, with a working link back to the clock. The smoke check reads the assembled license text. |
| Legacy config | Live centering converted to fixed longitude and automatic markers removed before any location loop. |
| Web regression | With the offline option omitted, the existing shared panel still presents online location and share controls; no live external service was called. |
| Fullscreen | Enter/exit exercised; SVG bounds stay inside the viewport. Screenshot visually inspected with the map and fixed marker visible and the aspect ratio preserved. The test uses software rendering for consistent captures. |
| Fullscreen exit icon (0.1.1) | Matching enter/exit SVG controls. Exit icon appears on entry and map interaction, resets its five-second timer on further interaction, fades and stops intercepting clicks when idle, reappears on movement, and exits fullscreen when clicked. Timer/reset/click behavior passed in the renderer; screenshot inspected. |
| Portable executable | Copied the actual EXE alone to a temporary directory outside the checkout, with spaces in its name and a fresh profile. It exited successfully after loading every bundled resource and checking renderer isolation/outbound denial. No development server was running. |
| Package contents | Inspected `app.asar`: only main process helpers, renderer resources, manifest/build info, licenses and stripped package metadata. No developer dependencies, tests, source checkout, personal settings or machine paths included. |
| Screenshots | Inspected the packaged cold-start map, night shading, clock/date and controls, plus the fullscreen development screenshot. Images/reports are ignored by Git. |
| Privacy | New source/documents use relative resource paths and generic contributor metadata. The implementation handoff plan was kept outside the contribution. Existing upstream public credits retained. |

## Reproduce

From the repository root:

```powershell
npm.cmd ci --prefix desktop --no-audit --no-fund
npm.cmd test --prefix desktop
npm.cmd run test:smoke --prefix desktop
npm.cmd run dist:win --prefix desktop
node desktop/test/packaged.cjs desktop/release/GeoClock-Offline-0.1.1-win-x64.exe
```

Build dependencies require internet access initially. Runtime resources are
bundled, and the app's session blocks external requests. Test reports and images
are written under `desktop/.verification/`; packaged checks use a fresh temporary
profile and clean it afterward. No personal profile is used.

## Remaining checks and limits

- No clean Windows VM or separate PC was available. Windows 11, a standard-user
  account and a physically disconnected network have not been independently
  tested. The fresh-profile packaged run used the application's network blocking
  policy on the connected development machine.
- Fullscreen pixels were checked in the development wrapper; the packaged
  diagnostic checked the normal window. Manual F11/Escape interaction in the
  packaged EXE and a long-duration idle/sleep/resume session remain to be checked.
- Individual timezone hover popups, every display size and every setting
  combination were not manually exercised. Both timezone datasets loaded locally;
  the planner rendered with the existing upstream code.
- The checks establish the recorded behavior, not a complete audit of Electron's
  upstream binaries or every npm transitive dependency. The app includes no
  telemetry/updater and makes no normal external service calls.
