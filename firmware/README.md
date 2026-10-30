# Flashing a ByteRelay firmware file

Firmware `.bin` files are distributed directly, not published in this repository — see the main
[README](../README.md#getting-the-firmware) for how to get one.

Once you have a file, you need [`esptool`](https://github.com/espressif/esptool) (`pip install esptool`)
and a USB cable to the device's UART/USB-OTG port (available for the first 120 seconds after power-up
only — after that the port is locked for security; power-cycle the device to flash again).

```bash
esptool.py --chip esp32s3 --port <YOUR_PORT> --baud 460800 write_flash \
  -z --flash_mode dio --flash_freq 80m --flash_size <8MB_or_16MB> \
  0x0 ByteRelay_<version>.bin
```

Replace `<YOUR_PORT>` with your serial port (e.g. `/dev/ttyUSB0`, `COM5`) and `<8MB_or_16MB>` with your
unit's flash size. Always verify the SHA-256 checksum you were given alongside the file before flashing.

> After flashing, the panel login and network settings reset to factory defaults
> (`admin` / `admin`, DHCP). Your relay names, scenes and schedules are kept.

Most owners never need this page — normal firmware updates happen from the web panel (System → Firmware
update), with automatic rollback if the new version doesn't start cleanly.
