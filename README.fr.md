---

# 📄 README.fr.md (FRANÇAIS)  
👉 **À copier-coller tel quel dans `README.fr.md`**

```markdown
# Horloge OLED Freebox Révolution (Raspberry Pi)

Ce projet permet de recréer l’affichage mythique de l’heure de la
**Freebox Révolution** à l’aide d’un Raspberry Pi et d’un petit écran OLED 128×64.

Il reprend les éléments emblématiques de cette horloge :
- une police “Freebox-like” recréée (chiffres en PNG)
- des animations fluides où les nouveaux chiffres glissent et chassent les anciens
- un affichage carré, simple et épuré

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
|-----:|--------------|
| VCC  | 3.3V ou 5V (selon le module) |
| GND  | GND |
| SDA  | GPIO2 (SDA) |
| SCL  | GPIO3 (SCL) |

Adresse I2C la plus courante : `0x3C`

---

## Préparation du Raspberry Pi

### Activer I2C

```bash
sudo raspi-config
# Options d’interface → I2C → Activer
sudo reboot
(Vérification optionnelle)

bash
Copier le code
sudo apt install -y i2c-tools
i2cdetect -y 1
Installation
Paquets système
bash
Copier le code
sudo apt update
sudo apt install -y python3-pip python3-pil
Dépendances Python
bash
Copier le code
pip3 install -r requirements.txt
Lancement
SH1106 (recommandé)
bash
Copier le code
python3 src/freebox_clock_sh1106.py
SSD1306 (ancien)
bash
Copier le code
python3 src/freebox_clock_ssd1306.py
Les fichiers de police doivent être présents dans :

bash
Copier le code
src/freeboxfont_/
Démarrage automatique (systemd)
Un service systemd est fourni dans le dossier systemd/.

Adapter les chemins si nécessaire

Installer le service :

bash
Copier le code
sudo cp systemd/freebox-clock.service /etc/systemd/system/freebox-clock.service
sudo systemctl daemon-reload
sudo systemctl enable freebox-clock
sudo systemctl start freebox-clock
Vérifier l’état :

bash
Copier le code
systemctl status freebox-clock
Remarques
Si l’écran reste noir, vérifier l’adresse I2C (0x3C dans la majorité des cas)

Vérifier que l’écran est bien en I2C (et non SPI)

La luminosité/contraste peut être ajustée dans le code
