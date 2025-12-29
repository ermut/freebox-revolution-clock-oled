# Freebox Revolution OLED Clock (Raspberry Pi)

Bring back the iconic **Freebox Revolution** clock display on modern hardware:
a Raspberry Pi + a small 128×64 OLED screen.

This project recreates:
- the **Freebox-like custom font** (PNG-based digits)
- the **smooth sliding / chasing transitions** when digits change
- a clean “square” look similar to the original Freebox Revolution clock

✅ Works with **SH1106 1.3" 128×64** (recommended)  
✅ Also supports **SSD1306 1.3" 128×64** (legacy / older modules)

---

## Demo
A short demo video is available in this repository.

---

## Hardware

- Raspberry Pi (Zero / 3 / 4 …)
- OLED 128×64 I2C (SH1106 or SSD1306)
- 4 wires: **VCC, GND, SDA, SCL**

### Wiring (I2C)

| OLED | Raspberry Pi |
|------|-------------|
| VCC  | 3.3V or 5V (depends on your module) |
| GND  | GND |
| SDA  | GPIO2 (SDA) |
| SCL  | GPIO3 (SCL) |

Typical I2C address: `0x3C`

---

## Raspberry Pi setup

### Enable I2C
```bash
sudo raspi-config
# Interface Options -> I2C -> Enable
sudo reboot
