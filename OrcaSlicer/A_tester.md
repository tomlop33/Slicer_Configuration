# Points à tester / incohérences connues

Ce document garde la trace des incohérences relevées par l'audit du 06/10/2026. Elles sont **volontairement laissées en l'état** en attendant des tests d'impression. Une fois les valeurs validées, les reporter dans les profils, puis retirer la section correspondante d'ici.

## 1. Pression d'avance (`pressure_advance`)

Il n'y a pas de logique d'ensemble :
- Seule l'**ANA 300** (et l'ANA 300G et la Lucy, qui partagent ses filaments) a des valeurs différentes par buse. Elles **augmentent** parfois avec la buse, alors que la pression d'avance diminue normalement quand le diamètre augmente.
- Les **HT, V2 et 600** ont presque partout 0.04, quelle que soit la buse.
- Les **EVA grosses buses** (1.2 / 2.5 / 3.0) ont 0 pour toutes les matières.
- Le **TPU** a 0.02 à 0.04, alors qu'il s'imprime normalement avec la pression d'avance désactivée.
- Certaines valeurs sont écrites `0.00` et d'autres `0` (Soluble, TPU sur V2 et 600).

Valeurs actuelles (profil compatible avec chaque machine et buse ; « — » = matière non proposée) :

| Matière | ANA 300 0.4 | ANA 300 0.6 | ANA 300 0.8 | HT 0.4 | HT 0.6 | HT 0.8 | V2 0.4 | V2 0.6 | V2 0.8 | 600 0.4 | 600 0.6 | 600 0.8 | EVA 0.4 | EVA 0.6 | EVA 0.8 | EVA 1.2-3.0 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| N-ABS | 0.03 | 0.02 | 0.03 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.03 | 0.02 | 0.02 | 0 |
| N-ABS-INDUS | 0.03 | 0.02 | 0.055 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.03 | 0.02 | 0.02 | 0 |
| N-ASA | 0.045 | 0.055 | 0.05 | 0.045 | 0.055 | 0.04 | 0.045 | 0.055 | 0.05 | 0.045 | 0.055 | 0.05 | 0.045 | 0.055 | 0.055 | 0 |
| N-BVOH | 0.03 | 0.02 | 0.035 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.035 | 0.04 | 0.04 | 0.035 | — | — | — | — |
| N-EASY FOOD | 0.03 | 0.05 | 0.035 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | — | — | — | — |
| N-EASY V0 | 0.03 | 0.05 | 0.035 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | — | — | — | — |
| N-PAHT CF | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0 |
| N-PC | 0.035 | 0.035 | 0.035 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.035 | 0.035 | 0.035 | 0 |
| N-PEEK | — | — | — | 0.04 | 0.04 | 0.04 | — | — | — | — | — | — | — | — | — | — |
| N-PEI | — | — | — | 0.04 | 0.04 | 0.04 | — | — | — | — | — | — | — | — | — | — |
| N-PETG | 0.055 | 0.04 | 0.045 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.055 | 0.04 | 0.04 | 0 |
| N-PETG-CF | 0.05 | 0.02 | 0.035 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.05 | 0.02 | 0.02 | 0 |
| N-PETG-ESD | 0.045 | 0.02 | 0.035 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | — | — | — | — |
| N-PETG-GF | 0.055 | 0.036 | 0.035 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.055 | 0.036 | 0.036 | 0 |
| N-PETG-GF UV | 0.045 | 0.055 | 0.045 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | — | — | — | — |
| N-PLA | 0.03 | 0.05 | 0.05 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.03 | 0.05 | 0.05 | 0 |
| N-PLX | 0.03 | 0.05 | 0.035 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.03 | 0.05 | 0.05 | 0 |
| N-PPA CF | 0.04 | 0.035 | 0.055 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.035 | 0.035 | 0 |
| N-PPS CF | 0.04 | 0.02 | 0.035 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.02 | 0.02 | 0 |
| N-PVA | 0.035 | 0.02 | 0.035 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | — | — | — | — |
| N-Soluble 111 | 0.03 | 0.02 | 0.055 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.00 | 0.04 | 0.04 | 0.00 | — | — | — | — |
| N-Soluble 150 | 0.03 | 0.02 | 0.055 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.00 | 0.04 | 0.04 | 0.00 | — | — | — | — |
| N-Soluble 90 | 0.03 | 0.02 | 0.055 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.00 | 0.04 | 0.04 | 0.00 | — | — | — | — |
| N-TPU | 0.03 | 0.02 | 0.055 | 0.04 | 0.04 | 0.04 | 0.04 | 0.04 | 0.00 | 0.04 | 0.04 | 0.00 | 0.03 | 0.02 | 0.02 | 0 |

**À tester** : test de calibration *Pressure advance* d'OrcaSlicer, par machine (vis à billes / courroie) et par buse, sur les matières principales (PLA, PETG, ABS, ASA, PC, CF).

## 2. Flow ratio (`filament_flow_ratio`)

Seule l'ANA 300 (avec l'ANA 300G et la Lucy) a des valeurs propres par buse : par exemple ABS 0.92 en 0.4 contre 0.95 ailleurs, Soluble et TPU 0.92 / 0.95 / 1 selon la buse. Les autres machines ont une valeur unique par matière.

| Matière | ANA 300 0.4 | ANA 300 0.6 | ANA 300 0.8 | HT 0.4 | HT 0.6 | HT 0.8 | V2 0.4 | V2 0.6 | V2 0.8 | 600 0.4 | 600 0.6 | 600 0.8 | EVA 0.4 | EVA 0.6 | EVA 0.8 | EVA 1.2-3.0 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| N-ABS | 0.92 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.92 | 0.95 | 0.95 | 0.95 |
| N-ABS-INDUS | 0.92 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.92 | 0.95 | 0.95 | 0.95 |
| N-ASA | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| N-BVOH | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | — | — | — | — |
| N-EASY FOOD | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | — | — | — | — |
| N-EASY V0 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | — | — | — | — |
| N-PAHT CF | 0.96 | 0.96 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.96 | 0.96 | 0.96 | 0.96 |
| N-PC | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 |
| N-PEEK | — | — | — | 1 | 1 | 1 | — | — | — | — | — | — | — | — | — | — |
| N-PEI | — | — | — | 1 | 1 | 1 | — | — | — | — | — | — | — | — | — | — |
| N-PETG | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 |
| N-PETG-CF | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 | 0.95 |
| N-PETG-ESD | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | — | — | — | — |
| N-PETG-GF | 0.93 | 0.93 | 0.93 | 0.93 | 0.93 | 0.93 | 0.93 | 0.93 | 0.93 | 0.93 | 0.93 | 0.93 | 0.93 | 0.93 | 0.93 | 0.93 |
| N-PETG-GF UV | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | — | — | — | — |
| N-PLA | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 |
| N-PLX | 0.98 | 0.98 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0.98 | 0.98 | 0.98 | 0.98 |
| N-PPA CF | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| N-PPS CF | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| N-PVA | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | 0.98 | — | — | — | — |
| N-Soluble 111 | 0.92 | 0.95 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | — | — | — | — |
| N-Soluble 150 | 0.92 | 0.95 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | — | — | — | — |
| N-Soluble 90 | 0.92 | 0.95 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | — | — | — | — |
| N-TPU | 0.92 | 0.95 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0.92 | 0.95 | 0.95 | 0.95 |

**À tester** : test de calibration *Flow rate* d'OrcaSlicer, par buse, sur une machine de chaque cinématique.

## 3. Autres points relevés (non bloquants)

- **Vitesses et accélérations des process au-dessus des limites machine** sur l'ANA 300, l'ANA 300G et la Lucy (vis à billes) :
  - déplacements à 500 mm/s pour une vitesse machine max de 150 ;
  - accélérations de 2 500 à 5 000 mm/s² pour un maximum machine de 1 500.

  OrcaSlicer ramène ces valeurs aux limites machine à l'impression, mais **l'estimation de durée est faussée**.
- **Lucy 300 en 0.20mm Strength** : réglée comme les machines à courroie (remplissage 150, paroi intérieure 80, gap fill 150). Sur tous les autres profils, elle suit l'ANA 300.
- **Paroi intérieure Strength** : 80 mm/s en buse 0.6 et 0.8, contre 125 mm/s en Standard et en Strength 0.4.
- **EVA** : accélération max X/Y à 600 mm/s², mais accélération max en extrusion à 6 000 mm/s². C'est sans effet réel, car la limite par axe s'applique à tous les mouvements.
- **EVA** : même rétraction (0.8 mm à 30 mm/s) et même z-hop (0.4 mm) de la buse 0.4 à la buse 3.0 (granulés).
- **PEI** : plateau à 220 °C, au-dessus de sa température de ramollissement (181 °C). OrcaSlicer affichera l'avertissement « ouvrir la porte / retirer le capot » à chaque découpage en PEI.

## Rappel : cinématiques

| Cinématique | Machines | Conséquence |
|---|---|---|
| Vis à billes | ANA 300, ANA 300G, Lucy 300, EVA | Accélérations faibles. Les profils Speed sont peu différents des Standard, c'est normal. |
| Courroie | ANA 300 HT, ANA 300 V2, ANA 600 | Accélérations et vitesses élevées. Les profils Speed sont nettement plus rapides. |
