# TiryaQLink Releases

Hosts release artifacts for the TiryaQLink app (Android APK and Windows installer EXE). Every release is created automatically by the [GitHub Actions workflow](.github/workflows/release.yml) when a `v<version>` tag (e.g. `v1.0.1`) is pushed.

## Permanent download URLs

These URLs always point to the **newest** release (the latest tag), so the app's `/app/version` endpoint can use them as fixed, never-changing links:

- **Android APK**
  `https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-1.0.1.apk`

- **Windows installer EXE**
  `https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-Setup-1.0.1.exe`

> Replace `1.0.1` with the version you are downloading. The `latest` part of the URL always resolves to the newest tagged release, so these links never need to be updated when a new version ships.

## How it works

1. Build artifacts are placed in `./dist` with the exact names:
   - `./dist/TiryaQLink-<version>.apk`
   - `./dist/TiryaQLink-Setup-<version>.exe`
2. Pushing a tag `v<version>` (matching `^v[0-9]+\.[0-9]+\.[0-9]+$`) triggers the release workflow.
3. The workflow creates a GitHub Release for that tag and attaches both files with those exact filenames.

See [USAGE.md](USAGE.md) for the step-by-step release process.
