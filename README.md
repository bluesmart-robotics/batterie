<!-- boardrepo-badge:v1 -->
[![View on BoardRepo](https://boardrepo.com/badge/github.svg?v=2)](https://boardrepo.com/b/def2d518-d971-4d70-adca-c127f0465930?ref=github-readme)
<!-- /boardrepo-badge:v1 -->

# batterie

Électronique du pack batterie du E-dolly : chargeur, carte écran et interface
vers le robot. Trois projets Altium, repris de
`BlueSmart_Robotics/Activités/R&D/Planeur/E-dolly/captronics/PCB/Batterie`.

## `chargeur_pmp41115/`

Chargeur dérivé du design de référence Texas Instruments **PMP41115** (240 W).
Schémas hiérarchiques en quatre feuilles :

| Feuille | Contenu |
|---|---|
| `1_240W SBD.SchDoc` | entrée 240 W, diode Schottky |
| `2_PD Control TPS26750.SchDoc` | négociation USB Power Delivery (TPS26750) |
| `3_BQ25756 Charger.SchDoc` | étage de charge (BQ25756), aussi en PDF |
| `4_PP5V Bias.SchDoc` | alimentation auxiliaire 5 V |

Plus `PMP41115.PcbDoc` (routage), `PMP41115 Main Board.PrjPcb`, `BOM.pdf`,
`layout_charger.png` et l'OutJob de validation.

## `pcb_ecran/`

Carte écran du pack, projet `PCB_Batterie_ESP` : schéma, routage, schéma en PDF
et quatre aperçus.

## `pcb_interface_robot/`

Carte d'interface entre le pack batterie et le robot, projet `PCB_interface` :
schéma, routage, nomenclature Altium, schéma en PDF et trois aperçus.

## Bibliothèques

Chaque projet référence ses bibliothèques **sans chemin**, donc Altium les
cherche dans le dossier du projet lui-même. Elles sont donc recopiées dans
chaque dossier qui en a besoin :

- `chargeur_pmp41115/` : `Batterie_components.SchLib`, `Batterie_footprint.PcbLib`,
  `PMP41115.PcbLib`, et le modèle 3D `BM04B-SRSS-TB.STEP`.
- `pcb_ecran/` : `Batterie_components.SchLib`, `Batterie_footprint.PcbLib`, et les
  modèles 3D `022032111.stp` et `B4B-PH-K-S.STEP`.
- `pcb_interface_robot/` : `Batterie_components.SchLib` et `PMP41115.PcbLib`.

Attention, les deux copies qui circulaient sur le poste de travail ont divergé :
`Batterie_components.SchLib` fait 351 744 octets du côté du chargeur et 364 544
du côté de la carte écran, et `Batterie_footprint.PcbLib` 2 039 808 contre
2 141 184. Chaque projet a donc reçu la copie avec laquelle il vivait, pour
qu'il s'ouvre tel quel. Il reste à fusionner ces deux versions en une seule
bibliothèque partagée, et à repointer les trois projets dessus.

Pour `pcb_interface_robot`, aucune bibliothèque n'accompagnait le projet sur le
poste : ce sont les copies du chargeur qui ont été retenues, par proximité de
famille. À vérifier à l'ouverture.
