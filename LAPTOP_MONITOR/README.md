# ESP-BOX-3 Laptop Monitor Firmware

ESP32-S3-BOX-3 firmware for:
- laptop status monitoring
- on-device schedule reminders
- local web settings page
- IR monitor
- simple games
- music control UI for internet radio / Spotify display flow

## Edit Wi-Fi And Device Settings

After flashing and booting the device, open the Box local settings page in a browser on the same network.

Use:
- `http://<device-ip>/settings`

On that page you can edit:
- `Wi-Fi SSID`
- `Wi-Fi Password`
- `Laptop IP`

Notes:
- `Laptop IP` is required.
- If you change Wi-Fi credentials, save them and then reboot the ESP once.
- Laptop IP changes apply to laptop status checks and sleep commands.

If the device is not fully configured yet, the screen will prompt:
- `Set Wi-Fi in /settings`

## Edit Music Settings

The firmware also exposes a local music control page:

- `http://<device-ip>/music`

From there you can edit:
- radio preset names
- radio preset URLs
- current music metadata
- Spotify connected state
- current preset
- volume label

The music API endpoints are:
- `GET /api/music`
- `POST /api/music`
- `POST /api/music/action`

## Launchpad Hosting

ESP Launchpad needs:
- `launchpad.toml`
- `bootloader.bin`
- `partition-table.bin`
- `ota_data_initial.bin`
- `gemini_voice_assistant.bin`

If hosting on GitHub Pages, make sure:
- `launchpad.toml` is publicly reachable
- the firmware binary URLs in `launchpad.toml` match the real hosted file paths exactly

Example Launchpad URL:

```text
https://espressif.github.io/esp-launchpad/?flashConfigURL=https://YOUR_SITE/launchpad.toml
```

## Backup Restore

The `backup/` folder contains the flashable firmware set and restore notes:
- [backup/README_FLASH.txt](C:/Users/evan/esp/gemini_voice_assistant/backup/README_FLASH.txt)
