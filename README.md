# SM64 Bob-omb Battlefield -> Android APK (GitHub Actions)

STATUS: nothing here has been built or run by the author. Only checked:
the workflow YAML parses, every shell step passes `bash -n`, and the
Bob-omb boot patch applies to the pinned source and passes a gcc
-fsyntax-only check. No APK exists until YOUR workflow run succeeds.

## What is used
- Source: github.com/VDavid003/sm64-port-android-base @ a71e0c11b7645ec401fcfc376295134f4e5e81b7
- Game:   github.com/VDavid003/sm64-port-android      @ b43af4667bd1cde0d6cb11004add92ffaffab1c5
  (sm64-port with SDL2 + OpenGL ES 2.0 and built-in touch controls)
- The workflow downloads both at build time; you only upload 2 things.

## Your private repo needs exactly
1. `.github/workflows/android.yml`   (the file from this chat)
2. `baserom.us.z64`                  (YOUR US ROM, big-endian, SHA-1 9bef1128717f958171a4afac3ed78ee2bb4e86ce)

## Phone steps
1. GitHub -> + -> New repository -> name it, choose **Private**, create.
2. In the repo: Add file -> Create new file. In the name box type
   `.github/workflows/android.yml` (typing `/` makes folders). Paste the
   full contents of android.yml. Commit.
3. Add file -> Upload files -> pick `baserom.us.z64` (must be exactly that
   name, ~8 MB) -> Commit.
4. Actions tab -> "Build SM64 Bob-omb Battlefield APK" -> Run workflow
   (a push to main also triggers it).
5. When it is green, open the run -> Artifacts -> `sm64-bob-debug-apk`.
   It downloads as a .zip: extract it with your Files app, then open
   `sm64-bob-debug.apk` and allow "install unknown apps" for your browser/Files.
6. If it fails, open the red step and send me its last ~50 lines.

## Behavior of this build
- Boots straight into Bob-omb Battlefield, act 1 (no intro, file select,
  castle or act select). The rest of the game is still inside the APK,
  because assets are extracted from the whole ROM. Falling out via death
  or "Exit Course" leads to castle grounds.
- Touch controls come from the upstream port (joystick, A, B, Z, R, C
  buttons, Start). Not tested by me.
- arm64-v8a only (most phones from ~2016 on).
- FPS: unknown until you run it. Report what you see and I'll tune.

## Legal
The APK contains assets extracted from your ROM. Keep the repo private,
don't share the APK or the artifact.
