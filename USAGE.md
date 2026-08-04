# Release process

## 1. Build the artifacts

Build both artifacts on your local machine and place them in `./dist` with these exact filenames:

- Android APK

  ```sh
  flutter build apk --release
  mkdir -p dist
  cp build/app/outputs/flutter-apk/app-release.apk dist/TiryaQLink-1.0.1.apk
  ```

- Windows installer (Inno Setup)

  Compile the existing `installer.iss` with Inno Setup so the output is named:

  ```text
  dist/TiryaQLink-Setup-1.0.1.exe
  ```

  (Set `OutputDir` and `OutputBaseFilename` in `installer.iss` accordingly.)

## 2. Tag the release

`dist/` is gitignored, so include the binaries in the release commit explicitly:

```sh
git add -f dist/TiryaQLink-1.0.1.apk dist/TiryaQLink-Setup-1.0.1.exe
git commit -m "Add build artifacts for v1.0.1"
git tag v1.0.1
git push origin main --tags
```

## 3. The workflow takes over

Pushing the `v1.0.1` tag triggers `.github/workflows/release.yml`. It:

1. Checks out the tagged commit.
2. Reads the version from the tag (`v1.0.1` -> `1.0.1`).
3. Creates a GitHub Release and attaches:
   - `TiryaQLink-1.0.1.apk`
   - `TiryaQLink-Setup-1.0.1.exe`

## 4. Download URLs go live

Once the release is published, these permanent links immediately point at the new version:

```text
https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-1.0.1.apk
https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-Setup-1.0.1.exe
```

`latest` always follows the newest tag, so the same URLs keep working for future releases.
