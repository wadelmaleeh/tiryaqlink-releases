# TiryaQLink Releases

Hosts the Windows release installer and Android APK for the TiryaQLink app. Every release is created automatically by the [GitHub Actions workflow](.github/workflows/release.yml) when a `v<version>` tag (e.g. `v1.0.4`) is pushed.

## Permanent download URLs

These URLs always point to the **newest** release (the latest tag), so the app's `/app/version` endpoint can use them as fixed, never-changing links:

- **Windows installer EXE**
  `https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-Setup-1.0.4.exe`

- **Android APK**
  `https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-1.0.4.apk`

> Replace `1.0.4` with the version you are downloading. The `latest` part of each URL always resolves to the newest tagged release, so these links never need to be updated when a new version ships.

## How it works

1. Release artifacts are built separately (e.g., by the main TiryaQLink project or in CI)
2. Build both artifacts with these exact filenames:
   - `./dist/TiryaQLink-Setup-<version>.exe` (Windows installer)
   - `./dist/TiryaQLink-<version>.apk` (Android APK)
3. Include these files in the release commit (they are normally gitignored but included with `git add -f dist/`) and push the tag `v<version>`:
   ```sh
   git add -f dist/TiryaQLink-Setup-<version>.exe dist/TiryaQLink-<version>.apk
   git commit -m "Add build artifacts for v<Version>"
   git tag v<Version>
   git push origin main --tags
   ```
4. Pushing the tag triggers `.github/workflows/release.yml`, which validates the artifacts exist in the tagged commit and creates a GitHub Release attaching both files.

See [USAGE.md](USAGE.md) for the step-by-step release process.