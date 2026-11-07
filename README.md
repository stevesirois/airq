# AirQ

An indoor air-quality monitor built around an ESP32-C6 and a [Sensirion SEN66](https://sensirion.com/products/catalog/SEN66) sensor, running [ESPHome](https://esphome.io/) and reporting into [Home Assistant](https://www.home-assistant.io/) that will cost you around 125$ (CAD).

The SEN66 is an all-in-one environmental sensor that measures:

- **CO₂** concentration
- **PM1.0 / PM2.5 / PM4.0 / PM10** particulate matter
- **Temperature** and **relative humidity**
- **VOC index** and **NOx index**

These values are published to Home Assistant as individual sensor entities over Wi-Fi, using ESPHome's native API.

## Project structure

| Path                                 | Purpose                                                         |
| ------------------------------------ | --------------------------------------------------------------- |
| `airq.yaml`                          | ESPHome config for the **WaveShare ESP32-C6-Zero / mini** board |
| `airqx.yaml`                         | ESPHome config for the **Seeed Studio XIAO ESP32-C6** board     |
| `airQ (PCB)/`                        | KiCad carrier/breakout PCB (ESP32-C6 + SEN66 headers)           |
| `3D-Print/`                          | 3D-printable enclosure (body, cover, TPU gasket) + assembly     |
| `BOM.ods`                            | Bill of materials spreadsheet                                   |
| `sensirion-datasheet-SEN6x-V1.0.pdf` | SEN66 sensor datasheet                                          |

## Hardware

- **MCU board:** either a
  - [WaveShare ESP32-C6-Zero / ESP32-C6 mini](https://www.espboards.dev/esp32/esp32-c6-zero-mini/) ([docs](https://docs.waveshare.com/ESP32-C6-Zero)), or a
  - [Seeed Studio XIAO ESP32C6](https://wiki.seeedstudio.com/xiao_esp32c6_getting_started/)
- **Sensor:** [Sensirion SEN66](https://sensirion.com/products/catalog/SEN66) (SEN6x family)
- **Carrier PCB:** a small breakout board (KiCad project in `airQ (PCB)/`) that hosts the ESP32-C6 board and the SEN66. Its headers are pin headers only — you solder the ESP32-C6 board and connect the sensor via its 6-pin cable. Manufacturable via [JLCPCB](https://jlcpcb.com/) using the files in `airQ (PCB)/production/`.
- **Enclosure:** 3D-printable body, cover, and TPU gasket (see `3D-Print/`), sized for the SEN66 with proper airflow openings (≥56 mm² inlet / ≥148 mm² outlet per Sensirion guidelines).

### Wiring (I²C)

| Board (config)                        | SCL    | SDA    |
| ------------------------------------- | ------ | ------ |
| WaveShare ESP32-C6-Zero (`airq.yaml`) | GPIO22 | GPIO21 |
| XIAO ESP32-C6 (`airqx.yaml`)          | GPIO23 | GPIO22 |

## Requirements

- **ESPHome** — see [esphome.io](https://esphome.io/) for installation. I suggest to use the executable version if you use Windows/MacOS or the AppImage if your are on Linux since this is the easiest way to use ESPHome

## Usage

1. Check the BOM.ods for all the required parts
2. Order your PCB from JLCPCB using the airQ.zip file that is ready for production
3. Depending of the controler used, short the 4 x 3 pins connectors accordingly on the PCB. The side mark "M" is for the Waveshare mini and the other side is for the Seeed XIAO (mark "X").
4. Print the enclosure
5. Configure and flash your controler using ESPHome. I put 2 yaml files that show the correct configuration for each board. The important part is the IO pin for the I²C interface vs the PCB board design
6. Assemble everything and hopefully it should work :-)

## Home Assistant dashboard for the sensor

To show the dashboard card (see picture in photo folder), install HACS (Home Assistant Community Store) and add the [Air Quality Card by KadenThomp36](https://github.com/KadenThomp36/Air-Quality-Card). The thresholds follow the WHO 2021 recommendations that this card also uses, so the recommendations on the device's display and the dashboard will stay consistent.

## Ordering / manufacturing

- **PCB:** upload the Gerber/drill files (the zip file) generated from `airQ (PCB)/production/airQ.zip` to [JLCPCB](https://jlcpcb.com/). The `production/` folder contains BOM and placement (CPL) exports for assembly.
- **Enclosure:** print the parts in `3D-Print/` (PLA body/cover, TPU for the gasket). See `3D-Print/README.md` for details.

## References

- [ESPHome](https://esphome.io/)
- [ESP32-C6-Zero — ESPBoards](https://www.espboards.dev/esp32/esp32-c6-zero-mini/)
- [ESP32-C6-Zero — WaveShare docs](https://docs.waveshare.com/ESP32-C6-Zero)
- [XIAO ESP32-C6 — ESPBoards](https://www.espboards.dev/esp32/xiao-esp32c6/)
- [XIAO ESP32-C6 — Seeed Studio wiki](https://wiki.seeedstudio.com/xiao_esp32c6_getting_started/)
- [Sensirion SEN66](https://sensirion.com/products/catalog/SEN66)
- [JLCPCB](https://jlcpcb.com/)
