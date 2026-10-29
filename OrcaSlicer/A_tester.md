# Points à tester / incohérences connues

Ce document garde la trace des incohérences relevées par l'audit du 06/10/2026. Elles sont **volontairement laissées en l'état** en attendant des tests d'impression. Une fois les valeurs validées, les reporter dans les profils, puis retirer la section correspondante d'ici.

## 1. Pression d'avance (`pressure_advance`)

État au 29/10/2026 :
- **Buse 0.4 : calibrée** pour toutes les matières, même valeur sur les ANA, la Lucy et les EVA 3DF05.
- **Buses 0.6 et 0.8 : estimations provisoires**, calculées à partir de la 0.4 : **0.6 = 0.7 × la valeur 0.4** et **0.8 = 0.5 × la valeur 0.4** (arrondi au millième). À vérifier par un test *Pressure advance* sur une machine par buse, puis à corriger ici.
- **EVA grosses buses** (3DF09 1.2 / 2.5, 3DP25 3.0) : 0 pour toutes les matières, à tester.
- **TPU** : 0 partout (dans `fdm_filament_tpu`).
Valeurs actuelles (profil compatible avec chaque machine et buse ; « — » = matière non proposée) :

| Matière | ANA 300 0.4 | ANA 300 0.6 | ANA 300 0.8 | HT 0.4 | HT 0.6 | HT 0.8 | V2 0.4 | V2 0.6 | V2 0.8 | 600 0.4 | 600 0.6 | 600 0.8 | EVA 0.4 | EVA 0.6 | EVA 0.8 | EVA 1.2-3.0 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| N-ABS | 0.02 | 0.014 | 0.01 | 0.02 | 0.014 | 0.01 | 0.02 | 0.014 | 0.01 | 0.02 | 0.014 | 0.01 | 0.02 | 0.014 | 0.01 | 0 |
| N-ABS-INDUS | 0.025 | 0.018 | 0.013 | 0.025 | 0.018 | 0.013 | 0.025 | 0.018 | 0.013 | 0.025 | 0.018 | 0.013 | 0.025 | 0.018 | 0.013 | 0 |
| N-ASA | 0.02 | 0.014 | 0.01 | 0.02 | 0.014 | 0.01 | 0.02 | 0.014 | 0.01 | 0.02 | 0.014 | 0.01 | 0.02 | 0.014 | 0.01 | 0 |
| N-BVOH | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | — | — | — | — |
| N-EASY FOOD | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | — | — | — | — |
| N-EASY V0 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | — | — | — | — |
| N-PAHT CF | 0.025 | 0.018 | 0.013 | 0.025 | 0.018 | 0.013 | 0.025 | 0.018 | 0.013 | 0.025 | 0.018 | 0.013 | 0.025 | 0.018 | 0.013 | 0 |
| N-PC | 0.035 | 0.025 | 0.018 | 0.035 | 0.025 | 0.018 | 0.035 | 0.025 | 0.018 | 0.035 | 0.025 | 0.018 | 0.035 | 0.025 | 0.018 | 0 |
| N-PEEK | — | — | — | 0.045 | 0.032 | 0.023 | — | — | — | — | — | — | — | — | — | — |
| N-PEI | — | — | — | 0.055 | 0.039 | 0.028 | — | — | — | — | — | — | — | — | — | — |
| N-PETG | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0 |
| N-PETG-CF | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0 |
| N-PETG-ESD | 0.065 | 0.046 | 0.033 | 0.065 | 0.046 | 0.033 | 0.065 | 0.046 | 0.033 | 0.065 | 0.046 | 0.033 | — | — | — | — |
| N-PETG-GF | 0.04 | 0.028 | 0.02 | 0.04 | 0.028 | 0.02 | 0.04 | 0.028 | 0.02 | 0.04 | 0.028 | 0.02 | 0.04 | 0.028 | 0.02 | 0 |
| N-PETG-GF UV | 0.04 | 0.028 | 0.02 | 0.04 | 0.028 | 0.02 | 0.04 | 0.028 | 0.02 | 0.04 | 0.028 | 0.02 | — | — | — | — |
| N-PLA | 0.04 | 0.028 | 0.02 | 0.04 | 0.028 | 0.02 | 0.04 | 0.028 | 0.02 | 0.04 | 0.028 | 0.02 | 0.04 | 0.028 | 0.02 | 0 |
| N-PLX | 0.045 | 0.032 | 0.023 | 0.045 | 0.032 | 0.023 | 0.045 | 0.032 | 0.023 | 0.045 | 0.032 | 0.023 | 0.045 | 0.032 | 0.023 | 0 |
| N-PPA CF | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0 |
| N-PPS CF | 0.01 | 0.007 | 0.005 | 0.01 | 0.007 | 0.005 | 0.01 | 0.007 | 0.005 | 0.01 | 0.007 | 0.005 | 0.01 | 0.007 | 0.005 | 0 |
| N-PVA | 0.035 | 0.025 | 0.018 | 0.035 | 0.025 | 0.018 | 0.035 | 0.025 | 0.018 | 0.035 | 0.025 | 0.018 | — | — | — | — |
| N-Soluble 111 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | — | — | — | — |
| N-Soluble 150 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | — | — | — | — |
| N-Soluble 90 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | 0.03 | 0.021 | 0.015 | — | — | — | — |
| N-TPU | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

**À tester** : voir le protocole de la section 4 (étape 2, pression d'avance) et la section 5 (pression d'avance adaptative, problème `M572 D0`).

## 2. Flow ratio (`filament_flow_ratio`)

Le flow ne dépend que de la **matière** (même tête sur toutes les ANA et Lucy, extrudeur calibré par machine). Il est donc défini **une seule fois par matière**, dans sa base `fdm_filament_<matière>`, et vaut la même chose sur toutes les machines et toutes les buses. Valeurs relevées le 28/10/2026 :

| Matière | Flow | Défini dans | État |
|---|---|---|---|
| N-PLA | 1 | `fdm_filament_pla` (= `fdm_filament_common`) | calibré 28/10/2026 (ANA/Lucy 0.4) |
| N-PLX | 0.98 | `fdm_filament_plx` | calibré 28/10/2026 (ANA/Lucy 0.4) |
| N-ABS | 0.98 | `fdm_filament_abs` | calibré 28/10/2026 (ANA/Lucy 0.4) |
| N-ABS-INDUS | 0.97 | `fdm_filament_abs_indus` | calibré 28/10/2026 (ANA/Lucy 0.4) |
| N-ASA | 0.98 | `fdm_filament_asa` | calibré 28/10/2026 (ANA/Lucy 0.4) |
| N-PAHT CF | 0.94 | `fdm_filament_paht_cf` | calibré 28/10/2026 (ANA/Lucy 0.4) |
| N-TPU | 1.08 | `fdm_filament_tpu` | calibré 28/10/2026 (ANA/Lucy 0.4) |
| N-PC | 0.95 | `fdm_filament_pc` | validé 29/10/2026 (valeur conservée) |
| N-PETG | 0.99 | `fdm_filament_petg` | calibré 28/10/2026 |
| N-PETG-CF | 0.95 | `fdm_filament_petg_cf` | calibré 28/10/2026 |
| N-PETG-GF | 0.99 | `fdm_filament_petg_gf` | calibré 28/10/2026 |
| N-PETG-GF UV | 0.99 | `fdm_filament_petg_gf_uv` | repris du N-PETG-GF le 29/10/2026 |
| N-PETG-ESD | 1.05 | `fdm_filament_petg_esd` | calibré 28/10/2026 |
| N-PPA CF | 0.78 | `fdm_filament_ppa` | calibré 29/10/2026 (paroi mesurée 1.16 mm pour 0.8897 mm attendus) |
| N-PPS CF | 0.97 | `fdm_filament_pps` | calibré 28/10/2026 |
| N-PEEK | 0.99 | `fdm_filament_peek` | calibré 28/10/2026 |
| N-PEI | 0.96 | `fdm_filament_pei` | calibré 29/10/2026 |
| N-BVOH | 1 | `fdm_filament_common` | validé 29/10/2026 (valeur conservée) |
| N-PVA | 0.98 | `fdm_filament_pva` | validé 29/10/2026 (valeur conservée) |
| N-EASY FOOD | 0.98 | `fdm_filament_easy_food` | validé 29/10/2026 (valeur conservée) |
| N-EASY V0 | 0.98 | `fdm_filament_easy_v0` | validé 29/10/2026 (valeur conservée) |
| N-Soluble 90 / 111 / 150 | 1 | `fdm_filament_common` | validé 29/10/2026 (valeur conservée) |
| Granulé (ANA 300G, tête 2) | 0.7 | `Namma Granulé @Namma ANA 300G` | à calibrer (extrusion à vis, pas comparable aux filaments) |
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
  - **EVA 3DF05** : traitée comme une ANA/Lucy (même flow et même pression d'avance par buse).
  - **EVA 3DF09 et 3DP25** : autres têtes (3DP25 à granulés) et filament de 2.85 mm. À mesurer séparément, au moins par type de tête.
  - **Buse** : l'effet du diamètre sur le flow est faible. Ne corriger une buse que si sa mesure s'écarte nettement.
  - **Machine sans chambre chaude** : le retrait peut y être différent. À vérifier.
- Pour la **pression d'avance**, la buse et la cinématique (vis à billes ou courroie) jouent davantage. Commencer par une valeur par matière, puis affiner par buse si nécessaire.

### Ordre des tests, pour chaque matière

1. **Flow** (méthode [Klippain — flow calibration](https://github.com/Frix-x/klippain/blob/main/docs/features/flow_calibration.md)) :
   - imprimer la coque creuse à parois connues (au moins 2 parois), retrait à 100 % ;
   - mesurer l'**épaisseur des parois** au micromètre ou au pied à coulisse, en plusieurs points, et faire la moyenne ;
   - calculer le multiplicateur d'extrusion et le reporter dans `filament_flow_ratio` ;
   - commencer par une ANA (référence), puis vérifier sur une Lucy et une EVA 3DF05 (mêmes valeurs attendues).
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
| N-ABS | ANA, Lucy et EVA 3DF05 0.4 (flow : toutes machines et buses) | 98 % | 0.02 | | | | 28/10/2026 : flow dans la base, PA dans les profils 0.4 |
| N-ABS-INDUS | ANA, Lucy et EVA 3DF05 0.4 (flow : toutes machines et buses) | 97 % | 0.025 | | | | 28/10/2026 : flow dans la base, PA dans les profils 0.4 |
| N-ASA | ANA, Lucy et EVA 3DF05 0.4 (flow : toutes machines et buses) | 98 % | 0.02 | | | | 28/10/2026 : flow dans la base, PA dans les profils 0.4 |
| N-PAHT CF | ANA, Lucy et EVA 3DF05 0.4 (flow : toutes machines et buses) | 94 % | 0.025 | | | | 28/10/2026 : flow dans la base, PA dans les profils 0.4 |
| N-PLA | ANA, Lucy et EVA 3DF05 0.4 (flow : toutes machines et buses) | 100 % | 0.04 | | | | 28/10/2026 : flow dans la base, PA dans les profils 0.4 |
| N-PLX | ANA, Lucy et EVA 3DF05 0.4 (flow : toutes machines et buses) | 98 % | 0.045 | | | | 28/10/2026 : flow dans la base, PA dans les profils 0.4 |
| N-TPU | ANA, Lucy et EVA 3DF05 0.4 (flow : toutes machines et buses) | 108 % | 0 | | | | 28/10/2026 : flow dans la base, PA dans les profils 0.4 |
| N-PPS CF | ANA, Lucy et EVA 3DF05 0.4 (flow : toutes machines et buses) | 97 % | 0.01 | | | | 28/10/2026 : flow dans la base, PA dans les profils 0.4 |
| N-PETG | ANA, Lucy et EVA 3DF05 0.4 (flow : toutes machines et buses) | 99 % | 0.03 | | | | 28/10/2026 : flow dans la base, PA dans les profils 0.4 |
| N-PETG-CF | ANA, Lucy et EVA 3DF05 0.4 (flow : toutes machines et buses) | 95 % | 0.03 | | | | 28/10/2026 : flow dans la base, PA dans les profils 0.4 |
| N-PETG-GF | ANA, Lucy et EVA 3DF05 0.4 (flow : toutes machines et buses) | 99 % | 0.04 | | | | 28/10/2026 : flow dans la base, PA dans les profils 0.4 |
| N-PETG-GF UV | ANA et Lucy 0.4 (flow : toutes machines et buses) | 99 % | 0.04 | | | | 29/10/2026 : valeurs reprises du N-PETG-GF (non mesurées) |
| N-PETG-ESD | ANA et Lucy 0.4 (flow : toutes machines et buses) | 105 % | 0.065 | | | | 28/10/2026 : flow dans la base, PA dans les profils 0.4 |
| N-PPA CF | ANA, Lucy et EVA 3DF05 0.4 (flow : toutes machines et buses) | 78 % | 0.03 | | | | 29/10/2026 : flow dans la base (paroi 1.16 mm pour 0.8897 attendus), PA dans les profils 0.4 |
| N-PC | ANA, Lucy et EVA 3DF05 0.4 (flow : toutes machines et buses) | 95 % | 0.035 | | | | 29/10/2026 : flow conservé, PA dans les profils 0.4 |
| N-PVA | ANA et Lucy 0.4 (flow : toutes machines et buses) | 98 % | 0.035 | | | | 29/10/2026 : flow conservé, PA dans les profils 0.4 |
| N-BVOH | ANA et Lucy 0.4 (flow : toutes machines et buses) | 100 % | 0.03 | | | | 29/10/2026 : flow conservé, PA dans les profils 0.4 |
| N-EASY FOOD | ANA et Lucy 0.4 (flow : toutes machines et buses) | 98 % | 0.03 | | | | 29/10/2026 : flow conservé, PA dans les profils 0.4 |
| N-EASY V0 | ANA et Lucy 0.4 (flow : toutes machines et buses) | 98 % | 0.03 | | | | 29/10/2026 : flow conservé, PA dans les profils 0.4 |
| N-Soluble 90 | ANA et Lucy 0.4 (flow : toutes machines et buses) | 100 % | 0.03 | | | | 29/10/2026 : flow conservé, PA dans les profils 0.4 |
| N-Soluble 111 | ANA et Lucy 0.4 (flow : toutes machines et buses) | 100 % | 0.03 | | | | 29/10/2026 : flow conservé, PA dans les profils 0.4 |
| N-Soluble 150 | ANA et Lucy 0.4 (flow : toutes machines et buses) | 100 % | 0.03 | | | | 29/10/2026 : flow conservé, PA dans les profils 0.4 |
| N-PEEK | ANA 300 HT 0.4 (flow : toutes buses) | 99 % | 0.045 | | | | 28/10/2026 : flow dans la base, PA dans le profil 0.4 |
| N-PEI | ANA 300 HT 0.4 (flow : toutes buses) | 96 % | 0.055 | | | | 29/10/2026 : flow dans la base, PA dans le profil 0.4 |

Une fois une matière validée : reporter les valeurs dans sa base `fdm_filament_<matière>`, **supprimer les surcharges** de flow et de pression d'avance devenues inutiles dans les profils machine et buse (sauf les écarts mesurés), puis retirer la matière des tableaux des sections 1 et 2.
## 5. Pression d'avance adaptative (`adaptive_pressure_advance`)

**Objectif.** Remplacer la pression d'avance fixe par un **modèle unique par matière (et par buse)**, valable pour toutes les machines puisqu'elles ont la même tête (Mosquito, LGX Pro, buse acier, même pas d'extrudeur). OrcaSlicer ajuste la valeur à chaque élément imprimé, selon son débit et son accélération :
- machines à vis à billes (ANA 300, 300G, Lucy, EVA) : bas du modèle, débits et accélérations faibles ;
- machines à courroie (HT, V2, 600) : haut du modèle.

Clés filament : `adaptive_pressure_advance` (activation), `adaptive_pressure_advance_model` (lignes `PA,débit mm³/s,accélération mm/s²`), `adaptive_pressure_advance_bridges` (PA sur les ponts), `adaptive_pressure_advance_overhangs` (expérimental). Garder une `pressure_advance` fixe raisonnable : elle sert de valeur de secours et au changement d'outil.

**⚠️ Bloquant pour les machines à 2 têtes : `M572 D0` en dur (confirmé).** Avec RepRapFirmware, OrcaSlicer (2.4.2, 2.5 alpha et 2.5 beta) envoie toujours `M572 D0 S…` quand il ne précise pas de tête : au changement d'outil, pour la pression d'avance adaptative et pendant les tests de calibration. Seuls les modes IDEX/IMEX de la 2.5 indiquent la tête. Quand la tête 2 (T1) imprime, la pression d'avance, fixe ou adaptative, est donc appliquée au **moteur de la tête 1**. Machines concernées : toutes les ANA, les EVA 3DF05, et les modes Copie/Miroir. La Lucy et les EVA 3DF09 et 3DP25 (une seule tête) ne sont pas concernées.
- Ticket OrcaSlicer : [#16204](https://github.com/OrcaSlicer/OrcaSlicer/issues/16204).
- **Correctif proposé : PR [#16913](https://github.com/OrcaSlicer/OrcaSlicer/pull/16913)** (ouverte le 27/10/2026, **pas encore mergée**, absente de la 2.5 beta). Sans tête précisée, `M572` vise maintenant la **tête active** (`T1` → `M572 D1 S…`). Rien ne change sur les machines à une tête (`D0`) ni sur les autres firmwares.
  - L'auteur n'a pas pu tester sur une machine Duet à deux têtes. **Test proposé sur une ANA**, avec une version qui contient la PR : découper une impression à 2 filaments et vérifier que `M572 D1 S<PA du filament 2>` suit chaque `T1` et que `M572 D0` suit chaque `T0`. Refaire le test avec la pression d'avance adaptative. Le résultat peut être posté en commentaire de la PR.
  - **Modes Copie/Miroir : non corrigés par la PR.** OrcaSlicer y voit une seule tête et enverra seulement `M572 D0`, alors que les outils `T2`/`T3` entraînent les deux moteurs. Le firmware doit continuer à régler le moteur 1, par exemple avec `M572 D0:1 S…` dans la macro de l'outil.
  - Une fois la PR publiée dans une version d'OrcaSlicer : retirer ce point bloquant (sauf pour les modes Copie/Miroir), supprimer le réglage de la tête 2 dans le firmware et lever la restriction de l'étape 5 ci-dessous.
- En attendant le correctif : la pression d'avance de la tête 2 vient du firmware (`config.g`, ou macro de changement d'outil `tpost1.g` avec `M572 D1 S…`), pas des profils.
- Contournement possible, **à tester** : dans le *Filament start G-code*, ajouter `M572 D[current_extruder] S{pressure_advance[current_extruder]}`. Cela corrigerait la valeur fixe au changement d'outil, mais pas le mode adaptatif.

**Protocole de calibration du modèle**, par matière et par buse, avec le flow déjà validé :
1. Sur une machine **à courroie** (pour couvrir les accélérations hautes) et **sur la tête 1**, lancer le test *Pressure advance* d'OrcaSlicer (motif) à **au moins 3 vitesses** : paroi externe, paroi interne, remplissage le plus rapide. Faire chaque vitesse à **2 accélérations** :
   - basse, environ 600 à 1 500 mm/s², comme les machines à vis à billes ;
   - haute, environ 5 000 à 7 000 mm/s², comme les machines à courroie.
2. Pour chaque test, noter la PA optimale et le **débit** affiché dans l'aperçu (schéma de couleur « Débit », curseur horizontal sur les lignes du motif). La PA optimale doit **diminuer** quand le débit augmente.
3. Écrire le modèle, une ligne par mesure (`PA,débit,accélération`), dans la base `fdm_filament_<matière>`, ou au niveau buse si les valeurs diffèrent selon la buse.
4. Vérifier sur une machine à vis à billes que le résultat est bon, sur une pièce de test et une pièce réelle.
5. N'activer `adaptive_pressure_advance` sur les machines à 2 têtes **qu'une fois le correctif `M572` publié** (PR #16913). D'ici là, l'activer seulement pour la Lucy et les EVA à une tête, ou pour des impressions sur la tête 1 uniquement.

| Matière | Buse | Lignes du modèle (`PA,débit,accél`) | Validé sur | Date / remarque |
|---|---|---|---|---|
| | | | | |

## 6. Rétraction (machines non EVA)

**Contexte.** Sur l'ANA, l'ANA 300G et la Lucy, presque toutes les matières reprennent les réglages de la machine : 0.8 mm à 35 mm/s, saut en Z de 0.4 mm en Normal Lift, essuyage activé. Font exception le PC, le PPA CF et le PPS CF, à 1 mm en Slope Lift. Ces valeurs ne sont pas calibrées par matière.

**Contraintes de la tête** (extrudeur direct LGX Pro, hotend Mosquito, buse en acier trempé) :
- plage habituelle d'un extrudeur direct : 0.4 à 1.2 mm, à 30-45 mm/s ;
- **ne pas dépasser 1.2 mm** : la zone de chauffe de la Mosquito est courte, et une rétraction plus longue ramène du plastique fondu dans le heatbreak, avec un risque de bouchage (surtout avec les matières chargées) ;
- la buse en acier trempé et les buses 0.6 / 0.8 suintent un peu plus : on ajoute couramment 0.1 à 0.2 mm par rapport à la buse 0.4.

**Avant de tester, deux prérequis :**
1. **Vérifier l'essuyage** : toutes les matières essuient sur 2 mm, avec 70 % de rétraction avant essuyage. Comparer avec 1 mm **avant** d'augmenter la longueur de rétraction.
2. **Sécher** les matières hygroscopiques (PETG, PA, PC, PVA, BVOH, Solubles) : un filament humide file quelle que soit la rétraction.

**Valeurs à tester :**

| Matière | Actuel | À tester | Raison |
|---|---|---|---|
| PETG, PETG-ESD | 0.8 mm / 35 mm/s | **1.0 mm**, 35-40 mm/s | Le PETG est la matière qui file le plus. |
| PETG-CF, PETG-GF, PETG-GF UV | 0.8 mm / 35 mm/s | **1.0 mm**, 35 mm/s | Il file comme le PETG. Rester à 1.0 mm au plus : les fibres usent les dents de l'extrudeur. |
| PAHT CF | 0.8 mm | **1.0 mm** | Le nylon file, surtout humide. |
| PEEK, PEI | 0.8 mm | **1.0 mm** | Suintement à très haute température. |
| PVA, BVOH, Soluble 90/111/150 | 0.8 mm / 35 mm/s | **1.0 mm**, 30 mm/s (**moins**) | Matières qui filent. Le PVA est cassant : baisser la vitesse. |
| TPU | 0.8 mm / 35 mm/s | **0.4-0.5 mm**, 20-25 mm/s (**moins**) | Une matière souple se comprime au lieu de se rétracter. Trop de rétraction la fait flamber dans l'extrudeur. |
| Granulé (tête 2 de l'ANA 300G) | 0.8 mm | selon l'extrudeur à granulés | Sur une vis, la rétraction agit peu. Jouer plutôt sur la température et l'essuyage. |
| PC, PPA CF, PPS CF | 1.0 mm | garder 1.0 mm | Déjà dans la bonne zone. |
| PLA, PLX, ABS, ABS-INDUS, ASA, EASY FOOD, EASY V0 | 0.8 mm | garder 0.8 mm | Adapté. |

**Protocole :**
1. Faire le flow et la pression d'avance **avant** la rétraction : une PA trop faible donne aussi des fils et des bavures.
2. Lancer le test de rétraction d'OrcaSlicer (menu Calibration, puis « Retraction test ») de 0.4 à 1.2 mm par pas de 0.1, sur la buse 0.4 d'une ANA, en commençant par le PETG.
3. Vérifier ensuite la valeur sur la buse 0.8 (ajouter 0.1 à 0.2 mm si nécessaire).
4. Reporter la valeur validée dans la base `fdm_filament_<matière>`, **uniquement pour les machines non EVA**. Les profils EVA gardent leurs propres valeurs, écrites dans chaque fichier.

| Matière | Buse | Essuyage retenu | Rétraction retenue (mm / mm/s) | Date / remarque |
|---|---|---|---|---|
| | | | | |

## 7. Autres points relevés (non bloquants)

- **Vitesses et accélérations des process au-dessus des limites machine** sur l'ANA 300, l'ANA 300G et la Lucy (vis à billes) :
  - déplacements à 500 mm/s pour une vitesse machine max de 150 ;
  - accélérations de 2 500 à 5 000 mm/s² pour un maximum machine de 1 500.

  OrcaSlicer ramène ces valeurs aux limites machine à l'impression, mais **l'estimation de durée est faussée**.
- **Profils Speed des EVA** : vitesses identiques aux profils Standard (seule la hauteur de couche change). Les profils Speed de l'ANA 300, de l'ANA 300G et de la Lucy sont proches des Standard, à cause des vis à billes.
- **EVA** : accélération max X/Y à 600 mm/s², mais accélération max en extrusion à 6 000 mm/s². C'est sans effet réel, car la limite par axe s'applique à tous les mouvements.
- **EVA** : même rétraction (0.8 mm à 30 mm/s) et même z-hop (0.4 mm) de la buse 0.4 à la buse 3.0 (granulés).

## Rappel : cinématiques

| Cinématique | Machines | Conséquence |
|---|---|---|
| Vis à billes | ANA 300, ANA 300G, Lucy 300, EVA | Accélérations faibles. Les profils Speed sont peu différents des Standard, c'est normal. |
| Courroie | ANA 300 HT, ANA 300 V2, ANA 600 | Accélérations et vitesses élevées. Les profils Speed sont nettement plus rapides. |
