# TiryaQLink Releases

Hosts the Windows release installer for the TiryaQLink app. Android is published on Google Play. Every release is created automatically by the [GitHub Actions workflow](.github/workflows/release.yml) when a `v<version>` tag (e.g. `v1.0.2`) is pushed.

## Permanent download URL

This URL always points to the **newest** release (the latest tag), so the app's `/app/version` endpoint can use it as a fixed, never-changing link:

- **Windows installer EXE**
  `https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-Setup-1.0.2.exe`

> Replace `1.0.2` with the version you are downloading. The `latest` part of the URL always resolves to the newest tagged release, so this link never needs to be updated when a new version ships.

## How it works

1. The installer is placed in `./dist` with the exact name:
   - `./dist/TiryaQLink-Setup-<version>.exe`
2. Pushing a tag `v<version>` (matching `^v[0-9]+\.[0-9]+\.[0-9]+$`) triggers the release workflow.
3. The workflow creates a GitHub Release for that tag and attaches the EXE with that exact filename.

See [USAGE.md](USAGE.md) for the step-by-step release process.
