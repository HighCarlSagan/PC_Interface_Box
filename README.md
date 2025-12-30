# PC Interface Box

A desktop information display and media control interface built around the ESP32-S3 microcontroller. The device provides a 3.5-inch TFT display for showing customizable content, physical controls for media playback, and multiple connectivity options for remote updates.

## Overview

The PC Interface Box serves as a dedicated desktop peripheral that combines display functionality with input controls. It connects to a host PC via USB-C for power and HID media control, while offering WiFi connectivity for remote content management and integration with home automation systems.

### Key Capabilities

- 480x320 pixel TFT display for text, graphics, and status information
- USB HID media controls (play, pause, next, previous, volume)
- Rotary encoder and tactile buttons for on-device navigation
- WiFi connectivity with on-device network configuration
- HTTP API for local network control
- MQTT support for remote messaging and home automation integration
- Over-the-air firmware updates
- Persistent local storage for multiple display screens

## Hardware Specifications

| Component | Specification |
|-----------|---------------|
| Microcontroller | ESP32-S3-WROOM-1-N8R8 |
| Display | 3.5" ILI9488 TFT, 480x320, SPI interface |
| Power | USB-C, 5V input |
| Wireless | WiFi 802.11 b/g/n 2.4GHz |
| Storage | 8MB Flash, 8MB PSRAM, 3.5MB SPIFFS |
| PCB | 100mm x 80mm, 2-layer |

### Input Controls

- 1x Rotary encoder with push button
- 3x Media control buttons (previous, play/pause, next)
- 5x Navigation buttons (up, down, left, right, select)
- 1x Mute button
- Boot and reset buttons for firmware updates

## Documentation

### Schematic

The full schematic is available as a PDF: [View Schematic](hardware/docs/schematic.pdf)

### Images

Device photos, PCB images, and UI screenshots are located in the `docs/images/` directory:

**Device Photos**
- `docs/images/device_front.jpg` - Front view of assembled device
- `docs/images/device_side.jpg` - Side profile view
- `docs/images/device_rear.jpg` - Rear view showing ports

**Hardware**
- `docs/images/pcb_top.jpg` - PCB top side
- `docs/images/pcb_bottom.jpg` - PCB bottom side
- `docs/images/pcb_3d_render.png` - KiCad 3D render

**User Interface**
- `docs/images/ui_home.png` - Home screen
- `docs/images/ui_wifi_setup.png` - WiFi configuration screen
- `docs/images/ui_settings.png` - Settings menu
- `docs/images/ui_cheatsheet.png` - Cheatsheet viewer
- `docs/images/ui_pcstats.png` - PC statistics display
- `docs/images/ui_calendar.png` - Calendar view

## Project Structure

```
PC_Interface_Box/
|
+-- hardware/                       # KiCad hardware design files
|   +-- pc_interface_box.kicad_pro  # KiCad project file
|   +-- pc_interface_box.kicad_sch  # Schematic
|   +-- pc_interface_box.kicad_pcb  # PCB layout
|   |
|   +-- libs/                       # Custom KiCad libraries
|   |   +-- symbols/                # Custom schematic symbols
|   |   +-- footprints/             # Custom PCB footprints
|   |
|   +-- docs/                       # Hardware documentation
|   |   +-- schematic.pdf           # Schematic PDF export
|   |   +-- bom.csv                 # Bill of materials
|   |   +-- assembly_notes.md       # Assembly instructions
|   |
|   +-- manufacturing/              # Production files
|   |   +-- gerbers/                # Gerber files for PCB fabrication
|   |   +-- bom_jlcpcb.csv          # BOM formatted for JLCPCB
|   |   +-- cpl_jlcpcb.csv          # Component placement for JLCPCB
|   |
|   +-- 3d-models/                  # 3D models for components
|       +-- step/                   # STEP files for enclosure design
|
+-- enclosure/                      # 3D printable enclosure
|   +-- enclosure.scad              # OpenSCAD parametric design
|   +-- parameters.scad             # Configurable dimensions
|   +-- top_shell.scad              # Top shell module
|   +-- bottom_shell.scad           # Bottom shell module
|   |
|   +-- export/                     # Export files for printing
|       +-- top_shell.stl           # Top shell STL
|       +-- bottom_shell.stl        # Bottom shell STL
|       +-- button_caps.stl         # Optional button caps
|
+-- companion/                      # PC companion application
|   +-- display_server.py           # Main server application
|   +-- requirements.txt            # Python dependencies
|   +-- config.example.yaml         # Example configuration
|   +-- systemd/                    # Systemd service files
|       +-- display-server.service
|
+-- docs/                           # Project documentation
|   +-- assembly_guide.md           # Step-by-step assembly
|   +-- user_manual.md              # End user documentation
|   +-- api_reference.md            # HTTP/MQTT API documentation
|   +-- troubleshooting.md          # Common issues and solutions
|   |
|   +-- images/                     # Documentation images
|       +-- device_front.jpg        # Assembled device photos
|       +-- device_side.jpg
|       +-- device_rear.jpg
|       +-- pcb_top.jpg             # PCB photos
|       +-- pcb_bottom.jpg
|       +-- pcb_3d_render.png       # KiCad 3D render
|       +-- ui_home.png             # UI screenshots
|       +-- ui_wifi_setup.png
|       +-- ui_settings.png
|       +-- ui_cheatsheet.png
|       +-- ui_pcstats.png
|       +-- ui_calendar.png
|
+-- .gitignore                      # Git ignore rules
+-- LICENSE                         # CERN-OHL-W-2.0 license
+-- README.md                       # This file
+-- CHANGELOG.md                    # Version history
```

## Hardware Design

The hardware design files are released under the CERN Open Hardware Licence Version 2 - Weakly Reciprocal (CERN-OHL-W-2.0). This permits use, modification, and distribution of the design while requiring that modifications to the hardware design files remain under the same license.

### Manufacturing

The PCB is designed for fabrication and assembly at JLCPCB or equivalent services. Manufacturing files include:

- Gerber files for PCB fabrication
- Bill of materials with JLCPCB part numbers
- Component placement file with correct rotations

To order from JLCPCB:

1. Upload the gerber ZIP file from `hardware/manufacturing/gerbers/`
2. Select assembly service and upload `bom_jlcpcb.csv` and `cpl_jlcpcb.csv`
3. Review component placement and confirm order

### Design Considerations

- USB differential pair routed with controlled impedance
- Thermal relief for voltage regulator with thermal vias
- Antenna keep-out zone maintained for WiFi performance
- ESD protection on USB data lines

### Bill of Materials

The complete BOM is available in `hardware/docs/bom.csv`. Key components:

| Component | Part Number | Package | Quantity |
|-----------|-------------|---------|----------|
| MCU | ESP32-S3-WROOM-1-N8R8 | LGA | 1 |
| LDO | AMS1117-3.3 | SOT-223 | 1 |
| ESD Protection | USBLC6-2SC6 | SOT-23-6 | 1 |
| Display | ILI9488 3.5" TFT | FPC 40-pin | 1 |
| USB Connector | USB-C 16-pin | SMD | 1 |
| Rotary Encoder | EC11 | SMD | 1 |

## Enclosure

The enclosure is designed for FDM 3D printing in PETG or ABS. Design files are provided in OpenSCAD format with parametric dimensions for customization.

### Printing Specifications

| Parameter | Value |
|-----------|-------|
| Material | PETG (recommended) or ABS |
| Layer Height | 0.2mm |
| Infill | 20% |
| Supports | Required for button cutouts |
| Print Time | Approximately 4-6 hours total |

### Assembly

The enclosure consists of two shells that snap together or are secured with M2.5 screws. Mounting bosses accept brass heat-set inserts for repeated assembly.

## Firmware

The firmware source code is not included in this repository. Pre-built firmware binaries may be provided in releases for flashing to assembled hardware.

For custom firmware development, the hardware uses:

- ESP-IDF framework (v5.1+)
- LVGL graphics library
- TinyUSB for USB functionality

### Flashing Pre-built Firmware

If firmware binaries are provided in releases:

```
# Install esptool
pip install esptool

# Flash firmware (adjust port as needed)
esptool.py --port /dev/ttyACM0 --baud 460800 write_flash 0x0 firmware.bin
```

## Assembly

Refer to `docs/assembly_guide.md` for detailed instructions. Overview:

1. Verify PCB assembly and inspect solder joints
2. Connect display via FPC cable
3. Flash firmware via USB
4. Assemble enclosure
5. Configure WiFi through device menu

## WiFi Configuration

The device supports on-device WiFi configuration without requiring firmware modification:

1. On first boot, navigate to the WiFi Setup screen
2. Select a network from the scanned list
3. Enter the password using the on-screen keyboard
4. Credentials are stored persistently in flash memory

Alternative configuration methods:

- Web-based setup via access point mode (connect to device AP, navigate to 192.168.4.1)
- USB serial commands (see API reference)

## Communication Interfaces

### USB HID

The device presents as a standard USB HID consumer control device. Media keys are sent directly to the host operating system without requiring drivers.

Supported controls: Play/Pause, Next Track, Previous Track, Volume Up/Down, Mute

### HTTP API

When connected to WiFi, the device runs an HTTP server on port 80. The API accepts JSON commands for updating display content and querying device status.

Example endpoints:

- `GET /api/status` - Device status and network info
- `POST /api/display` - Update display content
- `POST /api/brightness` - Adjust backlight

See `docs/api_reference.md` for complete documentation.

### MQTT

For remote control and home automation integration, the device can connect to an MQTT broker.

Topics:

- `display/{device_id}/cmd` - Commands to device
- `display/{device_id}/status` - Status from device

Supported brokers: Mosquitto, HiveMQ, EMQX, or any standard MQTT 3.1.1 broker.

## Companion Application

The optional PC companion application (`companion/display_server.py`) provides:

- System statistics monitoring (CPU, RAM, GPU temperature)
- Automatic display updates
- CLI for quick display commands
- MQTT bridge for remote sync

### Installation

```
cd companion
pip install -r requirements.txt
cp config.example.yaml config.yaml
python display_server.py
```

## Troubleshooting

Common issues and solutions are documented in `docs/troubleshooting.md`. Quick reference:

| Issue | Solution |
|-------|----------|
| Display not working | Check FPC cable orientation and connection |
| USB not recognized | Verify USB data lines, try different cable |
| WiFi won't connect | Check antenna clearance, verify credentials |
| Device runs hot | Verify thermal vias, reduce brightness |

## Version History

See `CHANGELOG.md` for detailed version history.

## License

Hardware design files (schematic, PCB, enclosure) are licensed under CERN-OHL-W-2.0. See LICENSE file for complete terms.

Firmware and software are not included in this repository and are not covered by this license.

## Contributing

Hardware contributions, bug reports, and documentation improvements are welcome. Please open an issue to discuss proposed changes before submitting modifications.

## Acknowledgments

This project uses the following open source tools and libraries:

- KiCad EDA for hardware design
- OpenSCAD for enclosure design
- ESP-IDF by Espressif Systems
- LVGL graphics library
