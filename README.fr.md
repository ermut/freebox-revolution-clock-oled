# Horloge OLED Freebox Révolution (Raspberry Pi)

Ce projet permet de recréer l’affichage mythique de l’heure de la
**Freebox Révolution** à l’aide d’un Raspberry Pi et d’un écran OLED 128×64.

Il reprend les éléments emblématiques de cette horloge :

- Police “Freebox-like” recréée (chiffres en PNG)
- Animations fluides où les nouveaux chiffres glissent et chassent les anciens
- Affichage carré, simple et épuré

Le projet a d’abord été développé pour les écrans SSD1306, puis migré vers
les écrans SH1106, aujourd’hui plus répandus et plus fiables.

---

## Démonstration

Une courte vidéo de démonstration est disponible dans ce dépôt.

---

## Matériel requis

- Raspberry Pi (Zero / 3 / 4 / etc.)
- Écran OLED 128×64 (I2C)
  - SH1106 (recommandé)
  - SSD1306 (ancien matériel)
- 4 fils : **VCC, GND, SDA, SCL**

### Câblage I2C

| OLED | Raspberry Pi |
|------|--------------|
| VCC  | 3.3V ou 5V (selon le module) |
| GND  | GND |
| SDA  | GPIO2 (SDA) |
| SCL  | GPIO3 (SCL) |

Adresse I2C la plus courante : `0x3C`

---

## Préparation du Raspberry Pi

### Activer I2C

    sudo raspi-config

- Options d’interface → I2C → Activer
- Redémarrer lorsque demandé

    sudo reboot

Vérification optionnelle :

    sudo apt install -y i2c-tools
    i2cdetect -y 1

---

## Installation

### Paquets système

    sudo apt update
    sudo apt install -y python3-pip python3-pil

### Dépendances Python

    pip3 install -r requirements.txt

---

## Lancement

### SH1106 (recommandé)

    python3 src/freebox_clock_sh1106.py

### SSD1306 (ancien)

    python3 src/freebox_clock_ssd1306.py

Les fichiers de police doivent être présents dans :

    src/freeboxfont_/

---

## Démarrage automatique (systemd)

Un service systemd est fourni dans le dossier `systemd/`.

1. Adapter les chemins si nécessaire
2. Installer le service :

    sudo cp systemd/freebox-clock.service /etc/systemd/system/freebox-clock.service
    sudo systemctl daemon-reload
    sudo systemctl enable freebox-clock
    sudo systemctl start freebox-clock

Vérifier l’état :

    systemctl status freebox-clock

---

## Remarques

- Si l’écran reste noir, vérifier l’adresse I2C
  (`0x3C` dans la majorité des cas)
- Vérifier que l’écran est bien en **I2C** (et non SPI)
- La luminosité / le contraste peuvent être ajustés dans le code
