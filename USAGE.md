# Release process (Windows)

Android is published through Google Play and is not part of this process.

## 1. Build the Windows installer

Compile the existing `installer.iss` with Inno Setup so the output is named:

```text
dist/TiryaQLink-Setup-1.0.2.exe
```

(Set `OutputDir` and `OutputBaseFilename` in `installer.iss` accordingly.)

## 2. Tag the release

`dist/` is gitignored, so include the binary in the release commit explicitly:

```sh
git add -f dist/TiryaQLink-Setup-1.0.2.exe
git commit -m "Add installer for v1.0.2"
git tag v1.0.2
git push origin main --tags
```

## 3. The workflow takes over

Pushing the `v1.0.2` tag triggers `.github/workflows/release.yml`. It:

1. Checks out the tagged commit.
2. Reads the version from the tag (`v1.0.2` -> `1.0.2`).
3. Creates a GitHub Release and attaches `TiryaQLink-Setup-1.0.2.exe`.

## 4. Download URL goes live

Once the release is published, this permanent link immediately points at the new version:

```text
https://github.com/wadelmaleeh/tiryaqlink-releases/releases/latest/download/TiryaQLink-Setup-1.0.2.exe
```

`latest` always follows the newest tag, so the same URL keeps working for future releases.
