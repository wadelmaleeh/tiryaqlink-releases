# TiryaQLink Releases

Hosts the Windows release installer and Android APK for the TiryaQLink app. Every release is created automatically by the [GitHub Actions workflow](.github/workflows/release.yml) when a `v<version>` tag (e.g. `v1.0.3`) is pushed.

## Permanent download URLs

These URLs always point to the **newest** release (the latest tag), so the app's `/app/version` endpoint can use them as fixed, never-changing links:

- **Windows installer EXE**
  `https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-Setup-1.0.3.exe`

- **Android APK**
  `https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-1.0.3.apk`

> Replace `1.0.3` with the version you are downloading. The `latest` part of each URL always resolves to the newest tagged release, so these links never need to be updated when a new version ships.

## How it works

1. The artifacts are placed in `./dist` with these exact names:
   - `./dist/TiryaQLink-Setup-<version>.exe`
   - `./dist/TiryaQLink-<version>.apk`
2. Pushing a tag `v<version>` (matching `^v[0-9]+\.[0-9]+\.[0-9]+$`) triggers the release workflow.
3. The workflow creates a GitHub Release for that tag and attaches both files with those exact filenames.

See [USAGE.md](USAGE.md) for the step-by-step release process.
