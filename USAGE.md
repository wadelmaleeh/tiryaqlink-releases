# Release process

## 1. Build the artifacts

### Android APK

Build with Flutter and copy to `./dist`:

```sh
flutter build apk --release
mkdir -p dist
cp build/app/outputs/flutter-apk/app-release.apk dist/TiryaQLink-1.0.3.apk
```

### Windows installer

Compile the existing `installer.iss` with Inno Setup so the output is named:

```text
dist/TiryaQLink-Setup-1.0.3.exe
```

(Set `OutputDir` and `OutputBaseFilename` in `installer.iss` accordingly.)

## 2. Tag the release

`dist/` is gitignored, so include the binaries in the release commit explicitly:

```sh
git add -f dist/TiryaQLink-1.0.3.apk dist/TiryaQLink-Setup-1.0.3.exe
git commit -m "Add artifacts for v1.0.3"
git tag v1.0.3
git push origin main --tags
```

## 3. The workflow takes over

Pushing the `v1.0.3` tag triggers `.github/workflows/release.yml`. It:

1. Checks out the tagged commit.
2. Reads the version from the tag (`v1.0.3` -> `1.0.3`).
3. Creates a GitHub Release and attaches:
   - `TiryaQLink-1.0.3.apk`
   - `TiryaQLink-Setup-1.0.3.exe`

## 4. Download URLs go live

Once the release is published, these permanent links immediately point at the new version:

```text
https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-1.0.3.apk
https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-Setup-1.0.3.exe
```

`latest` always follows the newest tag, so the same URLs keep working for future releases.
