# ESP-BOX-3 Laptop Monitor Firmware

ESP32-S3-BOX-3 firmware for:
- laptop status monitoring
- on-device schedule reminders
- local web settings page
- IR monitor
- simple games
- music control UI for internet radio / Spotify display flow

## First Network Setup

If the Box does not have a saved Wi-Fi SSID, or if normal Wi-Fi connection fails on boot, it falls back to provisioning mode automatically.

Provisioning mode starts a local hotspot:
- SSID: `ESP-BOX-3-Setup`
- Password: `configureme`

While connected to that hotspot, open either:
- `http://192.168.4.1/`
- `http://192.168.4.1/settings`

The root page redirects to the Wi-Fi setup page while provisioning mode is active.

Enter:
- `Wi-Fi SSID`
- `Wi-Fi Password`
- `Laptop IP`

Then press `Save Settings`.

The ESP will:
- store the settings
- reboot automatically
- try to join the entered Wi-Fi network

If the entered Wi-Fi is still unreachable on the next boot, the Box falls back to the setup hotspot again.

For a custom build, edit `sdkconfig.defaults` before building/flashing:

```ini
CONFIG_GEMINI_WIFI_SSID="YourWiFiName"
CONFIG_GEMINI_WIFI_PASSWORD="YourWiFiPassword"
CONFIG_GEMINI_LAPTOP_IP="192.168.1.13"
```

You can also change the same values through `menuconfig`.

Build-time defaults are still useful for:
- your own development firmware
- preconfigured private deployments
- testing without provisioning

There is no cloud AI setup required for this firmware.

## Edit Wi-Fi And Device Settings After The Box Is Online

Once the Box has joined your Wi-Fi network, open its local settings page from any device on the same network.

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
- If normal Wi-Fi fails later, the firmware falls back to provisioning hotspot mode again.
- The hotspot is only meant for setup and recovery; normal day-to-day changes can be done through the device IP on your Wi-Fi.

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

Important:
- `launchpad.toml` only tells Launchpad how to flash the firmware files.
- It does not collect Wi-Fi SSID/password from the end user.
- End-user Wi-Fi setup now happens after flashing through the built-in provisioning hotspot on the device.
- No API key is required for normal use of the firmware.

## Backup Restore

The published folder already contains the flashable firmware files directly:
- `bootloader.bin`
- `partition-table.bin`
- `ota_data_initial.bin`
- `gemini_voice_assistant.bin`
- `launchpad.toml`
