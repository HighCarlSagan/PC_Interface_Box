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

## Project Structure

```
PC_Interface_Box/
├── hardware/           KiCad schematic and PCB design files
│   ├── libs/           Custom symbols and footprints
│   ├── docs/           Schematic PDFs, design documentation
│   └── manufacturing/  Gerber files, BOM, pick-and-place data
├── enclosure/          3D printable enclosure design files
│   └── export/         STL files for printing
├── companion/          PC companion application (optional)
└── docs/               Assembly guide, user documentation
```

## Hardware Design

The hardware design files are released under the CERN Open Hardware Licence Version 2 - Weakly Reciprocal (CERN-OHL-W-2.0). This permits use, modification, and distribution of the design while requiring that modifications to the hardware design files remain under the same license.

### Manufacturing

The PCB is designed for fabrication and assembly at JLCPCB or equivalent services. Manufacturing files include:

- Gerber files for PCB fabrication
- Bill of materials with JLCPCB part numbers
- Component placement file with correct rotations

### Design Considerations

- USB differential pair routed with controlled impedance
- Thermal relief for voltage regulator with thermal vias
- Antenna keep-out zone maintained for WiFi performance
- ESD protection on USB data lines

## Enclosure

The enclosure is designed for FDM 3D printing in PETG or ABS. Design files are provided in OpenSCAD format with parametric dimensions for customization.

Recommended print settings:
- Layer height: 0.2mm
- Infill: 20%
- Material: PETG (preferred) or ABS
- Supports: Required for button cutouts

## Firmware

The firmware source code is not included in this repository. Pre-built firmware binaries may be provided in releases for flashing to assembled hardware.

For custom firmware development, the hardware uses:
- ESP-IDF framework
- LVGL graphics library
- TinyUSB for USB functionality

## Assembly

Refer to the assembly guide in the docs directory for step-by-step instructions on:

1. PCB assembly verification
2. Display connection
3. Enclosure assembly
4. Initial firmware flashing
5. WiFi configuration

## WiFi Configuration

The device supports on-device WiFi configuration without requiring firmware modification:

1. On first boot, navigate to the WiFi Setup screen
2. Select a network from the scanned list
3. Enter the password using the on-screen keyboard
4. Credentials are stored persistently in flash memory

Alternative configuration methods:
- Web-based setup via access point mode (192.168.4.1)
- USB serial commands

## Communication Interfaces

### USB HID

The device presents as a standard USB HID consumer control device. Media keys are sent directly to the host operating system without requiring drivers.

### HTTP API

When connected to WiFi, the device runs an HTTP server on port 80. The API accepts JSON commands for updating display content and querying device status.

### MQTT

For remote control and home automation integration, the device can connect to an MQTT broker. Topics follow the pattern:
- `display/{device_id}/cmd` - Commands to device
- `display/{device_id}/status` - Status from device

## License

Hardware design files (schematic, PCB, enclosure) are licensed under CERN-OHL-W-2.0. See LICENSE file for details.

## Contributing

Hardware contributions, bug reports, and documentation improvements are welcome. Please open an issue to discuss proposed changes before submitting modifications.

## Acknowledgments

This project uses the following open source components:
- ESP-IDF by Espressif Systems
- LVGL graphics library
- KiCad EDA
