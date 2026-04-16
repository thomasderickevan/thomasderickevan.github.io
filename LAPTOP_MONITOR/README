ESP firmware backup created from the current build output.

Files included:
- bootloader.bin
- partition-table.bin
- ota_data_initial.bin
- gemini_voice_assistant.bin
- flasher_args.json
- flash_args.txt

Typical restore command:
python -m esptool --chip esp32s3 --before default_reset --after hard_reset write_flash --flash_mode dio --flash_freq 80m --flash_size 16MB 0x0 bootloader.bin 0x8000 partition-table.bin 0xd000 ota_data_initial.bin 0x10000 gemini_voice_assistant.bin

If you use ESP-IDF tools, you can also adapt the command from flash_args.txt.
