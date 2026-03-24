# ChronIQ Firmware Releases

Firmware binaries and update manifest for ChronIQ wearable devices.

## How it works

1. The ChronIQ app fetches `manifest.json` from GitHub Pages to check for updates
2. If a newer version is available, the app downloads the `.bin` from the GitHub Release
3. The firmware is uploaded to the device over BLE using MCUmgr SMP

## Releasing a new firmware version

```bash
# 1. Build and sign the firmware (produces app_update.bin)
# 2. Compute SHA256
sha256sum app_update.bin

# 3. Create a GitHub release with the binary attached
gh release create v1.0.0 app_update.bin --title "v1.0.0" --notes "Release notes here"

# 4. Update manifest.json with new version, URL, and SHA256
# 5. Commit and push manifest.json
```

## Manifest format

```json
{
  "latest_version": "1.0.0",
  "min_app_version": "1.0.0",
  "firmware_url": "https://github.com/CharlesMod/chroniq-firmware-releases/releases/download/v1.0.0/app_update.bin",
  "sha256": "abcdef1234567890...",
  "release_notes": "What changed in this version"
}
```

The app fetches `https://charlesmod.github.io/chroniq-firmware-releases/manifest.json`
