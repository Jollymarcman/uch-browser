# Browser performance mode

## Changes

- The Pages entry screen asks the player to choose Normal or Performance before the Unity loader starts.
- Normal uses the existing player defaults and the browser's normal device-pixel ratio.
- Performance adds `?uchMode=performance`, then a browser-only startup adapter applies the recovered project's `Low` quality profile, enforces texture mip limit 2, disables VSync, and targets 30 fps. The page also caps device-pixel ratio at 0.75 to shrink the render buffer.
- The adapter is new compatibility code in `Assets/Compatibility/UCHWebPerformanceMode.cs`. Original gameplay scripts and the Steam installation were not changed.

## Build evidence

- Unity: 2021.3.45f1, WebGL, Development build, Size code optimization.
- Build output: `UCH-WebGL-MovementDiagnostics-20261123-220843`.
- Unity BuildReport: Succeeded, 0 build errors, 554 warnings; reported total size 902,958,003 bytes.
- Player files: `.data` 183,201,210 bytes; `.wasm` 113,214,052 bytes; `.framework.js` 752,712 bytes; loader 26,036 bytes.
- The generated IL2CPP C++ and `.data` contain the adapter's `UCHPerformanceMode` code and log strings.
- `StreamingAssets/Audio` (605,288,050 bytes) and `StreamingAssets/PS4` were omitted from the Pages copy, matching the previous offline WebGL deployment. The source project files remain untouched.

## Memory limits

Performance mode reduces render-buffer use and mipmapped texture memory, but it does not impose a WebAssembly heap ceiling or remove the required scene/data payload. The current import metadata has 47 mipmapped textures and 187 without mipmaps, so the texture reduction may be limited. Unity 2021.3 documents that the WebGL heap may grow to 2 GB, that the `.data` file is unpacked into browser memory, and that `PlayerSettings.WebGL.memorySize` has no effect on WebAssembly. A substantial total-RAM reduction would require a separate asset-loading/build design and measurement; this mode should not be described as a guaranteed fix for a 2 GB freeze.

## Verification status

The Unity player build succeeded. A browser run of this updated player has not yet been verified.
