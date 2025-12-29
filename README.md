# Freebox Revolution OLED Clock (Raspberry Pi)

Bring back the iconic **Freebox Revolution** clock display on modern hardware  
using a Raspberry Pi and a small 128×64 OLED screen.

This project recreates the legendary Freebox clock:

- Custom Freebox-like font (PNG-based digits)
- Smooth sliding / chasing animations when digits change
- Clean, square and minimalist layout

Originally developed for SSD1306 OLED displays, the project was later migrated  
to SH1106 displays (more common and reliable today).

---

## Demo

A short demonstration video is available in this repository.

---

## Hardware requirements

- Raspberry Pi (Zero / 3 / 4 / etc.)
- OLED display 128×64 (I2C)
  - SH1106 (recommended)
  - SSD1306 (legacy)
- 4 wires: **VCC, GND, SDA, SCL**

### I2C wiring

| OLED | Raspberry Pi |
|------|--------------|
| VCC  | 3.3V or 5V (depends on module) |
| GND  | GND |
| SDA  | GPIO2 (SDA) |
| SCL  | GPIO3 (SCL) |

Typical I2C address: `0x3C`

---

## Raspberry Pi setup

### Enable I2C

```bash
sudo raspi-config


Interface Options → I2C → Enable

Reboot when prompted

sudo reboot


Optional check:

sudo apt install -y i2c-tools
i2cdetect -y 1

Installation
System packages
sudo apt update
sudo apt install -y python3-pip python3-pil

Python dependencies
pip3 install -r requirements.txt

Run
SH1106 (recommended)
python3 src/freebox_clock_sh1106.py

SSD1306 (legacy)
python3 src/freebox_clock_ssd1306.py


The custom font images must be located in:

src/freeboxfont_/

Autostart at boot (systemd)

A systemd service file is provided in the systemd/ directory.

Edit paths inside the service file if needed

Install the service:

sudo cp systemd/freebox-clock.service /etc/systemd/system/freebox-clock.service
sudo systemctl daemon-reload
sudo systemctl enable freebox-clock
sudo systemctl start freebox-clock


Check status:

systemctl status freebox-clock

Notes

If the display stays blank, verify the I2C address
(0x3C is common, sometimes 0x3D)

Make sure your OLED module is I2C (not SPI)

Contrast/brightness can be adjusted in the code
