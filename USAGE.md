# Release process

The release workflow builds all artifacts automatically in GitHub Actions. You only need to create a tag:

## 1. Create a tag

Push a `v<version>` tag to trigger the release workflow:

```sh
git tag v1.0.4
git push origin main --tags
```

The tag must match the regex `^v[0-9]+\.[0-9]+\.[0-9]+$` (e.g., `v1.0.4`).

## 2. Workflow builds artifacts automatically

When the tag is pushed, `.github/workflows/release.yml` runs:

### Android APK
- Sets up Flutter
- Runs `flutter build apk --release`
- Saves artifact as `dist/TiryaQLink-<version>.apk`

### Windows installer
- Installs Inno Setup
- Compiles `installer.iss` (version placeholder `@VERSION@` is replaced)
- Saves artifact as `dist/TiryaQLink-Setup-<version>.exe`

Both artifacts are attached to the GitHub Release with exact filenames.

## 3. Download URLs go live

Once the release is published, these permanent links immediately point at the new version:

```text
https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-1.0.4.apk
https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-Setup-1.0.4.exe
```

`latest` always follows the newest tag, so the same URLs keep working for future releases.
