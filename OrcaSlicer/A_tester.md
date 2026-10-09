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

**À tester** : voir le protocole de la section 4 (étape 2, pression d'avance) et la section 5 (pression d'avance adaptative, problème `M572 D0`).

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

**À tester** : voir le protocole de la section 4 (étape 1, flow).

## 3. Retrait (`filament_shrink`)

Le retrait compense la **contraction du plastique en refroidissant**. Cette contraction est **proportionnelle à la taille de la pièce** : en ABS, environ 2 mm sur 300 mm et environ 7 mm sur 1 000 mm. Une calibration du flow ne la corrige pas, car elle ne mesure que l'épaisseur des parois. Les deux réglages sont complémentaires.

Valeurs actuelles (définies dans les bases `fdm_filament_<matière>`, communes à toutes les machines) :

| Matière | Retrait XY actuel |
|---|---|
| N-ABS, N-ABS-INDUS, N-PC | 99.325 % |
| N-ASA | 99.53 % |
| N-PETG, N-PETG-CF, N-PETG-GF, N-PETG-ESD | 99.7 % |
| N-PETG-GF UV | 99.6 % |
| N-PAHT CF, N-PPA CF | 99.9 % |
| Autres (PLA, PLX, PPS CF, PEEK, PEI, TPU, solubles, EASY, Granulé) | 100 % (pas de compensation) |

Le retrait en Z (`filament_shrinkage_compensation_z`) est à 100 % partout.

**À tester** : voir le protocole de la section 4 (étape 3, retrait).

## 4. Protocole de calibration

### Principe : une valeur par matière, pas par machine

- **ANA et Lucy** ont la même tête : hotend Mosquito, extrudeur LGX Pro, buse en acier trempé. Le **flow** et la **pression d'avance** dépendent alors surtout de la matière, à condition que le pas de l'extrudeur (`rotation_distance` dans le firmware) soit **calibré sur chaque machine** avant les tests. Ce pas est un réglage machine, pas filament.
- Le **retrait** est une propriété de la matière, influencée surtout par la température de chambre.
- Les valeurs validées vont donc **dans les bases `fdm_filament_<matière>`**, communes à toutes les machines. On ne crée de surcharge, dans le profil modèle ou buse, que si un test montre un écart réel :
  - **EVA** : autres têtes (3DF05, 3DF09, 3DP25 à granulés) et filament de 2.85 mm. À mesurer séparément, au moins par type de tête.
  - **Buse** : l'effet du diamètre sur le flow est faible. Ne corriger une buse que si sa mesure s'écarte nettement.
  - **Machine sans chambre chaude** : le retrait peut y être différent. À vérifier.
- Pour la **pression d'avance**, la buse et la cinématique (vis à billes ou courroie) jouent davantage. Commencer par une valeur par matière, puis affiner par buse si nécessaire.

### Ordre des tests, pour chaque matière

1. **Flow** (méthode [Klippain — flow calibration](https://github.com/Frix-x/klippain/blob/main/docs/features/flow_calibration.md)) :
   - imprimer la coque creuse à parois connues (au moins 2 parois), retrait à 100 % ;
   - mesurer l'**épaisseur des parois** au micromètre ou au pied à coulisse, en plusieurs points, et faire la moyenne ;
   - calculer le multiplicateur d'extrusion et le reporter dans `filament_flow_ratio` ;
   - commencer par une ANA (référence), puis vérifier sur une Lucy et une EVA 3DF05.
2. **Pression d'avance** : test *Pressure advance* d'OrcaSlicer, avec le flow validé, sur les buses utilisées. Valeur dans `pressure_advance`.
3. **Retrait**, avec le flow validé :
   - imprimer une **grande pièce** (barre ou cube de 100 à 200 mm, plus grand sur ANA 600 et EVA) avec `filament_shrink` à **100 %**, la chambre à sa température habituelle et la pièce refroidie à température ambiante ;
   - mesurer en X et en Y ;
   - calculer `retrait = cote mesurée / cote nominale × 100` (exemple : 198.6 / 200 → **99.3 %**) ;
   - si X et Y diffèrent, prendre la moyenne et noter l'écart ;
   - reporter la valeur dans `filament_shrink`.
4. **Ajustements fins**, si besoin, sur des pièces fonctionnelles : `xy_contour_compensation` et `xy_hole_compensation` (process). Ils corrigent un **décalage fixe** des contours et des trous, pas le retrait.

### Relevé des résultats

| Matière | Machine / buse | Flow mesuré | Pression d'avance | Retrait X | Retrait Y | Retrait retenu | Date / remarque |
|---|---|---|---|---|---|---|---|
| | | | | | | | |

Une fois une matière validée : reporter les valeurs dans sa base `fdm_filament_<matière>`, **supprimer les surcharges** de flow et de pression d'avance devenues inutiles dans les profils machine et buse (sauf les écarts mesurés), puis retirer la matière des tableaux des sections 1 et 2.
## 5. Pression d'avance adaptative (`adaptive_pressure_advance`)

**Objectif.** Remplacer la pression d'avance fixe par un **modèle unique par matière (et par buse)**, valable pour toutes les machines puisqu'elles ont la même tête (Mosquito, LGX Pro, buse acier, même pas d'extrudeur). OrcaSlicer ajuste la valeur à chaque élément imprimé, selon son débit et son accélération :
- machines à vis à billes (ANA 300, 300G, Lucy, EVA) : bas du modèle, débits et accélérations faibles ;
- machines à courroie (HT, V2, 600) : haut du modèle.

Clés filament : `adaptive_pressure_advance` (activation), `adaptive_pressure_advance_model` (lignes `PA,débit mm³/s,accélération mm/s²`), `adaptive_pressure_advance_bridges` (PA sur les ponts), `adaptive_pressure_advance_overhangs` (expérimental). Garder une `pressure_advance` fixe raisonnable : elle sert de valeur de secours et au changement d'outil.

**⚠️ Bloquant pour les machines à 2 têtes : `M572 D0` en dur (confirmé).** Avec RepRapFirmware, OrcaSlicer 2.4.2 envoie toujours `M572 D0 S…`. Quand la tête 2 (T1) imprime, la pression d'avance, fixe ou adaptative, est donc appliquée au **moteur de la tête 1**. Machines concernées : toutes les ANA, les EVA 3DF05, et les modes Copie/Miroir. La Lucy et les EVA 3DF09 et 3DP25 (une seule tête) ne sont pas concernées.
- Ticket OrcaSlicer : [#16204](https://github.com/SoftFever/OrcaSlicer/issues/16204), à suivre. Retirer ce point bloquant une fois le correctif publié.
- En attendant le correctif : la pression d'avance de la tête 2 vient du firmware (`config.g`, ou macro de changement d'outil `tpost1.g` avec `M572 D1 S…`), pas des profils.
- Contournement possible, **à tester** : dans le *Filament start G-code*, ajouter `M572 D[current_extruder] S{pressure_advance[current_extruder]}`. Cela corrigerait la valeur fixe au changement d'outil, mais pas le mode adaptatif.

**Protocole de calibration du modèle**, par matière et par buse, avec le flow déjà validé :
1. Sur une machine **à courroie** (pour couvrir les accélérations hautes) et **sur la tête 1**, lancer le test *Pressure advance* d'OrcaSlicer (motif) à **au moins 3 vitesses** : paroi externe, paroi interne, remplissage le plus rapide. Faire chaque vitesse à **2 accélérations** :
   - basse, environ 600 à 1 500 mm/s², comme les machines à vis à billes ;
   - haute, environ 5 000 à 7 000 mm/s², comme les machines à courroie.
2. Pour chaque test, noter la PA optimale et le **débit** affiché dans l'aperçu (schéma de couleur « Débit », curseur horizontal sur les lignes du motif). La PA optimale doit **diminuer** quand le débit augmente.
3. Écrire le modèle, une ligne par mesure (`PA,débit,accélération`), dans la base `fdm_filament_<matière>`, ou au niveau buse si les valeurs diffèrent selon la buse.
4. Vérifier sur une machine à vis à billes que le résultat est bon, sur une pièce de test et une pièce réelle.
5. N'activer `adaptive_pressure_advance` sur les machines à 2 têtes **qu'une fois le correctif `M572` publié**. D'ici là, l'activer seulement pour la Lucy et les EVA à une tête, ou pour des impressions sur la tête 1 uniquement.

| Matière | Buse | Lignes du modèle (`PA,débit,accél`) | Validé sur | Date / remarque |
|---|---|---|---|---|
| | | | | |
## 6. Autres points relevés (non bloquants)

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
