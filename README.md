# Dama Master — Universal Checkers Solver ♛

Single-file checkers/dama solver implementing **Moroccan Dama rules**, packaged as an Android app.

## Moroccan Dama rules (implemented 100%)

- Men move 1 step diagonally **forward**; capture forward **and backward**
- **Mandatory capture** with the **MAX capture rule** (longest path forced) — `findMaxCaptureLength()`
- Flying kings (bishop-like): land on any empty square beyond the captured piece, chained captures
- Promotion ends the turn immediately, even if the new king could keep capturing

## Engine (`index.html`, self-contained)

- `getAllCaptures(board, r, c, player)` — recursion + backtracking, explores all branches
- `getAllMoves()` — legal moves with mandatory/max-capture filtering
- `minimax()` with α-β pruning, depth 1–15

## Features

- Play vs engine (White or Black), or 2-player analysis board
- Variant dropdown (Moroccan max-capture / International any-capture), who starts, depth slider
- **Analyze**: lists all possibilities sorted with evals, capture counts, **BEST** badge + arrow highlight
- Capture rule toggle: mandatory, or optional with the **huffing** rule (remove the piece that should have taken, or ignore)

## Web
Open `index.html` in any browser. No build, no dependencies, fully offline.

## Android APK (GitHub Actions)

The repo is a minimal Android (Gradle + WebView) project — no Cordova/Capacitor/npm needed.

**Build an APK automatically:**

1. Go to the **Actions** tab → **Build Android APK** → **Run workflow** (or just push to `main`)
2. When the run finishes, download the **DamaMaster-APK** artifact
3. Install `app-debug.apk` or `app-release.apk` on your device (allow "install unknown apps")

**Publish a release:** push a tag — `git tag v1.0 && git push --tags` — and the workflow attaches both APKs to a GitHub Release.

CI details:

- JDK 17 (Temurin) + Gradle 8.7 + Android Gradle Plugin 8.4.0, `compileSdk 34`, `minSdk 21`
- `index.html` is copied into `app/src/main/assets/` at build time — single source of truth, edit the web app only
- The release APK is signed with the debug keystore so it installs on devices; add your own `signingConfigs` in `app/build.gradle` for Play Store publishing

## Test position

White king d4, Black men e5 & f6, White to move → press **Test Position** then **Analyze**: White wins by force by capturing both men (zugzwang — every black reply walks into a capture).

## Repo layout

```
index.html                          # the entire solver (engine + UI)
android project:
├── app/build.gradle
├── app/src/main/AndroidManifest.xml
├── app/src/main/java/.../MainActivity.java   # WebView shell
├── build.gradle / settings.gradle / gradle.properties
└── .github/workflows/android.yml  # CI: builds & publishes APKs
```
