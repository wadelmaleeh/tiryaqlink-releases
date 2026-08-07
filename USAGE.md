# Release process

Releases are created from pre-built artifacts. The workflow does **not** build anything — it only attaches artifacts that are committed into the release tag.

## 1. Build the artifacts

Build both files in the TiryaQLink project and copy them to `./dist` with these exact names:

- Windows installer (produced by the existing Inno Setup script `installer.iss`):

  ```text
  ./dist/TiryaQLink-Setup-1.0.4.exe
  ```

- Android APK:

  ```sh
  flutter build apk --release
  cp build/app/outputs/flutter-apk/app-release.apk ./dist/TiryaQLink-1.0.4.apk
  ```

## 2. Commit and tag

`dist/` is gitignored, so include the binaries in a release commit explicitly:

```sh
git add -f ./dist/TiryaQLink-1.0.4.apk ./dist/TiryaQLink-Setup-1.0.4.exe
git commit -m "Add build artifacts for v1.0.4"
git tag v1.0.4
git push origin main --tags
```

The tag must match `^v[0-9]+\.[0-9]+\.[0-9]+$` (e.g. `v1.0.4`).

## 3. Workflow creates the release

Pushing the `v1.0.4` tag triggers `.github/workflows/release.yml`, which validates that `./dist/TiryaQLink-Setup-1.0.4.exe` and `./dist/TiryaQLink-1.0.4.apk` exist in the tagged commit, then creates a GitHub Release attaching both files with those exact filenames.

## 4. Download URLs go live

Once the release is published, these permanent links immediately point at the new version:

```text
https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-1.0.4.apk
https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-Setup-1.0.4.exe
```

`latest` always follows the newest tag, so the same URLs keep working for future releases.