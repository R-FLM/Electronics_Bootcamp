# 42uino mini — Bootcamp Électronique : Design

Carte de développement compatible Arduino (format Pro Mini) à base d'ATmega328P cadencé à 16 MHz, conçue sous KiCad avec des bibliothèques de symboles et d'empreintes personnalisées, selon les règles de fabrication JLCPCB.

| Livrable | Fichier |
|---|---|
| Bibliothèque de symboles | [First_lib.kicad_sym](First_kicad_proj/First_lib.kicad_sym) |
| Bibliothèque d'empreintes | [first_fp_lib.pretty/](First_kicad_proj/first_fp_lib.pretty) |
| Schéma | [First_kicad_proj.kicad_sch](First_kicad_proj/First_kicad_proj.kicad_sch) |
| Layout PCB | [First_kicad_proj.kicad_pcb](First_kicad_proj/First_kicad_proj.kicad_pcb) |
| Export PDF du schéma | [Bootcamp_elec_flomulle_schematic.pdf](First_kicad_proj/Bootcamp_elec_flomulle_schematic.pdf) |
| Export PDF du PCB | [Bootcamp_elec_flomulle_pcb_layout.pdf](First_kicad_proj/Bootcamp_elec_flomulle_pcb_layout.pdf) |

## Nomenclature (BOM)

17 composants. Les liens renvoient aux fiches produit Mouser référencées dans chaque empreinte, d'où l'on accède à la datasheet.

| Réf. | Qté | Valeur | Boîtier | Référence fabricant | Rôle | Datasheet |
|---|---|---|---|---|---|---|
| U1 | 1 | ATmega328P-AN | TQFP-32 | Microchip ATMEGA328P-AN | Microcontrôleur | [Mouser](https://www.mouser.fr/en/ProductDetail/Microchip-Technology/ATMEGA328P-AN?qs=6Dg1WZIWLC6WK556tw8xAw%3D%3D) |
| Y1 | 1 | 16 MHz | 3225 (4 pads) | Kyocera AVX CX3225SA16000D0PSTZ1 | Quartz d'horloge | [Mouser](https://www.mouser.fr/en/ProductDetail/KYOCERA-AVX/CX3225SA16000D0PSTZ1?qs=DN1kgsm7Y2SRgzHPt1S5hg%3D%3D) |
| C1, C2 | 2 | 12 pF | 0603 | Murata GRM1885C2E120FW07J | Capacités de charge du quartz | [Mouser](https://www.mouser.fr/en/ProductDetail/Murata-Electronics/GRM1885C2E120FW07J?qs=d0WKAl%252BL4KbD%2Ff0qK%252BVCeQ%3D%3D) |
| C3, C4, C7 | 3 | 100 nF | 0603 | Vishay Vitramon GA0603Y104MBXAR31G | C3 : filtrage AREF · C4 : auto-reset (DTR → RST) · C7 : découplage VCC | [Mouser](https://www.mouser.fr/en/ProductDetail/Vishay-Vitramon/GA0603Y104MBXAR31G?qs=uwxL4vQweFMKFiCe6YWxnw%3D%3D) |
| C6 | 1 | 1 µF | 0603 | Taiyo Yuden MSASE168SB5105KTNA01 | Découplage VCC | [Mouser](https://www.mouser.fr/en/ProductDetail/TAIYO-YUDEN/MSASE168SB5105KTNA01?qs=yc9RBI4tIAKZAWDraq01Cw%3D%3D) |
| R1 | 1 | 330 Ω | 0603 | Royalohm 0603WAF3300T5E | Limitation de courant de la LED D1 | [Mouser](https://www.mouser.fr/en/ProductDetail/Royalohm/0603WAF3300T5E?qs=sGAEpiMZZMtlubZbdhIBIDH%2FP7BvsepRJZVZEYBKqDw%3D) |
| R2, R3 | 2 | 10 kΩ | 0603 | Littelfuse TFR0603BHC1002NR | R2 : limitation de courant de la LED D2 · R3 : pull-up de RESET | [Mouser](https://www.mouser.fr/en/ProductDetail/Littelfuse/TFR0603BHC1002NR?qs=wT7LY0lnAe3f1NNuny8WOw%3D%3D) |
| D1 | 1 | Verte | 0603 | Lumex SML-LX0603SGW-TR | LED utilisateur sur D13 (SCK) | [Mouser](https://www.mouser.fr/en/ProductDetail/Lumex/SML-LX0603SGW-TR?qs=sGAEpiMZZMvVL5Kk7ZYykWS6taeFwoCBY0eyA%252B5ssLk%3D) |
| D2 | 1 | Rouge | 0603 | Lumex SML-LX0603IW-TR | Témoin d'alimentation | [Mouser](https://www.mouser.fr/en/ProductDetail/Lumex/SML-LX0603IW-TR?qs=sGAEpiMZZMvVL5Kk7ZYykVwAM0Y%252B7BnPfXWhOQRjJ7w%3D) |
| SW1 | 1 | B3U-1000P | SMD | B3U-1000P | Bouton RESET | [Mouser](https://www.mouser.fr/en/ProductDetail/Aratas/B3U-1000P?qs=AO7BQMcsEu4ip80xyf2FwA%3D%3D) |
| J1, J2 | 2 | 1×12 | THT 2,54 mm, droit | TE Connectivity 1-826629-2 | Barrettes d'E/S latérales | [Mouser](https://www.mouser.fr/en/ProductDetail/TE-Connectivity/1-826629-2?qs=FazuUmncXokmxpv%252BFZO3KQ%3D%3D) |
| J3 | 1 | 1×06 | THT 2,54 mm, coudé | Amphenol FCI 10129379-906002BLF | Connecteur de programmation FTDI | [Mouser](https://www.mouser.fr/en/ProductDetail/Amphenol-FCI/10129379-906002BLF?qs=0lQeLiL1qyajiejozaUUsw%3D%3D) |

## Brochage (pinout)

### J1 — barrette 1×12

| Broche | Signal | ATmega (port / broche, fonctions alternatives) | Fonction |
|---|---|---|---|
| 1 | D9 | PB1 / 13 (PCINT1/OC1A) | E/S numérique, PWM |
| 2 | D8 | PB0 / 12 (PCINT0/CLKO/ICP1) | E/S numérique |
| 3 | D7 | PD7 / 11 (PCINT23/AIN1) | E/S numérique |
| 4 | D6 | PD6 / 10 (PCINT22/OC0A/AIN0) | E/S numérique, PWM |
| 5 | D5 | PD5 / 9 (PCINT21/OC0B/T1) | E/S numérique, PWM |
| 6 | D4 | PD4 / 2 (PCINT20/XCK/T0) | E/S numérique |
| 7 | D3 | PD3 / 1 (PCINT19/OC2B/INT1) | E/S numérique, PWM, INT1 |
| 8 | D2 | PD2 / 32 (PCINT18/INT0) | E/S numérique, INT0 |
| 9 | GND | GND / 3, 5, 21 | Masse |
| 10 | RST | PC6 / 29 (RESET/PCINT14) | Reset (actif bas) |
| 11 | RXI | PD0 / 30 (PCINT16/RXD) | UART RX |
| 12 | TXO | PD1 / 31 (PCINT17/TXD) | UART TX |

### J2 — barrette 1×12

| Broche | Signal | ATmega (port / broche, fonctions alternatives) | Fonction |
|---|---|---|---|
| 1 | RAW | VCC / 4, 6 · AVCC / 18 | Alimentation 5 V |
| 2 | GND | GND / 3, 5, 21 | Masse |
| 3 | RST | PC6 / 29 (RESET/PCINT14) | Reset (actif bas) |
| 4 | RAW | VCC / 4, 6 · AVCC / 18 | Alimentation 5 V |
| 5 | A3 | PC3 / 26 (ADC3/PCINT11) | Entrée analogique / E/S |
| 6 | A2 | PC2 / 25 (ADC2/PCINT10) | Entrée analogique / E/S |
| 7 | A1 | PC1 / 24 (ADC1/PCINT9) | Entrée analogique / E/S |
| 8 | A0 | PC0 / 23 (ADC0/PCINT8) | Entrée analogique / E/S |
| 9 | SCK (D13) | PB5 / 17 (PCINT5/SCK) | SPI SCK, LED verte D1 |
| 10 | MISO (D12) | PB4 / 16 (PCINT4/MISO) | SPI MISO |
| 11 | MOSI (D11) | PB3 / 15 (PCINT3/OC2A/MOSI) | SPI MOSI, PWM |
| 12 | D10 | PB2 / 14 (PCINT2/SS/OC1B) | E/S numérique, PWM, SPI SS |

### J3 — connecteur FTDI 1×06

| Broche | Signal | ATmega (port / broche, fonctions alternatives) |
|---|---|---|
| 1 | DTR | PC6 / 29 (RESET/PCINT14), via C4 |
| 2 | TXO | PD1 / 31 (PCINT17/TXD) |
| 3 | RXI | PD0 / 30 (PCINT16/RXD) |
| 4 | RAW | VCC / 4, 6 · AVCC / 18 |
| 5 | GND | GND / 3, 5, 21 |
| 6 | GND | GND / 3, 5, 21 |

### Broches de l'ATmega sans connections
- PC4 / 27 (ADC4/SDA/PCINT12) et PC5 / 28 (ADC5/SCL/PCINT13), soit A4/A5 et donc le bus I²C ;
- ADC6 / 19 et ADC7 / 22, soit A6/A7 ;
- PB6 / 7 (PCINT6/XTAL1/TOSC1) et PB7 / 8 (PCINT7/XTAL2/TOSC2), occupées par le quartz Y1.
