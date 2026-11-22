# Ultimate Chicken Horse browser playtest

Public browser test site for the recovered Unity WebGL build. Original game code and game assets are copyright Clever Endeavour Games and their respective rights holders. The project owner reports receiving permission from the rights holder to publish this build for testing. This is an unofficial test build and is not affiliated with Clever Endeavour Games.

This repository uses Git LFS for Unity's large `.data` and `.wasm` build files. GitHub Actions checks out the LFS content and deploys only `site/` to GitHub Pages. The `site` folder is based on the Unity WebGL output from Unity 2021.3.45f1, build `UCH-WebGL-MovementDiagnostics-20261122-205732`.

The deployment copy omits Windows Wwise soundbanks and PS4-only streaming assets. The WebGL build has no browser-compatible Wwise native plugin, so those platform-specific files do not provide browser audio. The original Unity output remains preserved separately.

Once the Pages workflow completes, open the site URL shown in the GitHub Actions deployment summary. The online directory is configured in the build; hosts still need the multiplayer service online for friends to join.
