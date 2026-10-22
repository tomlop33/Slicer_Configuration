# Changelog — Profils Namma OrcaSlicer

## 22/10/2026 — version 01.01.02.00 (modifications du 12/10 au 21/10/2026)

Bundle : `Namma 22_10_2026.zip` (`Namma.json` + `Namma/`). Il remplace `Namma 09_10_2026.zip`.

> Certains réglages (`top_surface_expansion`, ordre « Best of all ») n'existent que depuis **OrcaSlicer 2.5** : les versions antérieures les ignorent ou reviennent à la valeur par défaut.

### Modifications
- **Débit max** (`filament_max_volumetric_speed`) : N-PETG-CF, N-PETG-GF, N-PETG-GF UV et N-PETG-ESD passent à 15 mm³/s (au lieu de 20), sur ANA, Lucy et EVA 3DF05. Les EVA 3DF09 et 3DP25 restent à 75 mm³/s.
- **N-PEI** (ANA 300 HT) : plateau à 160 °C (au lieu de 220 °C, qui dépassait la température de ramollissement de 181 °C). La fiche technique Namma N-PEI 9085 indique une plage de 140 à 220 °C (essais réalisés à 140 °C). OrcaSlicer n'affiche plus l'avertissement « ouvrir la porte » en PEI.
  - Réglages alignés sur la fiche technique : ventilateur de pièce coupé (0 %, surplombs et ponts compris, au lieu de 10-40 %), débit max 5.4 mm³/s (au lieu de 10, soit environ 60 mm/s en buse 0.4 et couche 0.2, pour une vitesse conseillée de 30 à 60 mm/s), buse à 360 °C (au lieu de 355 °C, température des essais mécaniques).
- **Process, tous les profils** (`fdm_process_common`) :
  - « Precise wall » (`precise_outer_wall`) désactivé.
  - « Precise Z height » (`precise_z_height`) activé.
  - « Top surface expansion » (`top_surface_expansion`) à 10 mm. Ce réglage n'existe que depuis OrcaSlicer 2.5 : les versions antérieures l'ignorent.
  - « Align directions to model » (`align_infill_direction_to_model`) activé.
  - Lissage du débit d'extrusion (100 mm³/s², inchangé) appliqué seulement aux parois externes et aux surplombs (`extrusion_rate_smoothing_external_perimeter_only`). Option disponible depuis OrcaSlicer 2.4.
  - Générateur de parois Arachne : « Wall distribution count » à 2 (au lieu de 1).
  - Ponts : débit à 1.1 en externe et en interne (au lieu de 1.35), densité à 110 % en externe et en interne (au lieu de 100 %). OrcaSlicer multiplie le débit interne par le débit externe : le débit réel des ponts internes est donc de 1.21 (au lieu de 1.82).
  - Parois supplémentaires sur les surplombs (`extra_perimeters_on_overhangs`) activées.
  - Ordre dans la couche (`print_order`) : « Best of all (shortest path) » (au lieu de Default). Valeur ajoutée dans OrcaSlicer 2.5 : les versions antérieures reviennent à Default.
- **Start G-code ANA et Lucy** : l'appel à `start_print_ANA.g` / `start_print_Lucy.g` transmet le diamètre de buse de T0 et T1 (`D` / `F`) et le filament découpé de T0 et T1 (`K` / `L`, valeur de `filament_notes`). Sur les ANA, `K` et `L` ne sont envoyés que pour les têtes utilisées. En modes Copie et Miroir, les deux têtes reçoivent la buse et le filament de T0. La Lucy reçoit seulement `D` et `K`.
- **Notes des filaments** (`filament_notes`) : chaque matière contient le nom de son filament dans le firmware Duet (dossiers `0:/filaments/` du dépôt `01_common`), par exemple `N-ABS INDUS`, `N-PETG_CF` ou `Granule`. Ce nom servira à vérifier que le filament chargé dans la machine correspond à celui du découpage.
- **Refroidissement, toutes les matières** : vitesse minimale d'impression (`slow_down_min_speed`) à 5 mm/s (au lieu de 10 mm/s), et seuil de ventilation des surplombs (`overhang_fan_threshold`) à 50 % (au lieu de 25 %, 95 % ou 0 % selon la matière). Les deux valeurs sont définies une seule fois, dans `fdm_filament_common`.
- **Type de saut en Z** (toutes les machines) : Auto Lift pour toutes les matières. Les ANA et la Lucy étaient en Normal Lift, sauf N-PC, N-PPA CF et N-PPS CF en Slope Lift. Les EVA étaient en Slope Lift pour la plupart des matières, et en Normal Lift pour N-PLX, N-PETG-CF, N-PETG-GF et N-TPU. Le type est défini une seule fois par machine (`fdm_*_common`). Avec l'arc fitting désactivé, OrcaSlicer écrit la spirale en segments G1, sans G2/G3.
- **Vitesses des profils Strength** :
  - ANA 300, ANA 300G et Lucy 300 (vis à billes) : les Strength 0.6 et 0.8, et le Strength 0.4 de la Lucy, reprennent les vitesses du Standard de même buse (paroi intérieure 125 mm/s, remplissage 100, gap fill 80, dessus 85, support 80). Ils étaient plus rapides que le Standard sur le remplissage et plus lents sur les parois.
  - EVA 500 et 1000 (buses 0.4, 0.6 et 0.8) : les Strength reprennent les vitesses du Standard (déplacements 150 mm/s au lieu de 500, remplissage 100, plein interne 100, gap fill 50, dessus 90, support 60). Ils étaient plus rapides que les profils Speed.
  - ANA 300 HT, ANA 300 V2 et ANA 600 (courroie) : inchangés.
- **Vitesses des buses 0.6, 0.8 et 1.0 sur les machines à courroie** (ANA 300 HT, ANA 300 V2, ANA 600) : le dessus passe à 100 mm/s (au lieu de 150) et le remplissage à 150 mm/s (au lieu de 100), comme en buse 0.4. Cela concerne les profils Quality 0.6 et 0.8, Standard et Strength 0.8, Standard 1.0 de l'ANA 600, et le dessus du Speed 0.6.
- **Température de chambre** : N-ABS, N-ABS-INDUS, N-ASA, N-PC, N-PPA CF, N-PPS CF et N-Soluble 150 passent à 60 °C (au lieu de 65 °C), en minimale comme en cible. Cela s'applique à toutes les machines, ANA 300 HT et EVA comprises, sauf là où la HT a sa propre valeur (PC, PPA CF, PPS CF, Soluble 150).
  - ANA 300 HT : N-ABS, N-ABS-INDUS et N-ASA à 65 °C, N-PAHT CF à 75 °C (au lieu de 60 °C).
- **Ponts épais internes** (`thick_internal_bridges`, tous les process) : désactivés. Les ponts internes sont maintenant imprimés à la hauteur de couche, comme les ponts externes.
- **N-PC** : température de ramollissement (`temperature_vitrification`) à 140 °C au lieu de 110 °C, plus proche de la transition vitreuse réelle du PC. OrcaSlicer n'affiche plus l'avertissement « ouvrir la porte » avec le plateau à 120 °C.
- **Ventilation** :
  - N-PEEK et N-PEI : surplombs et ponts à 40 % au lieu de 100 %, comme leur ventilation maximale.
  - N-PETG-CF, N-PETG-GF, N-PETG-GF UV et N-PETG-ESD : alignés sur le PETG. Ventilation 10-60 % (au lieu de 35-100 %), seuil des surplombs 25 % (au lieu de 95 %), durée de couche pour la ventilation 30 s (au lieu de 60), ralentissement sous 3 s (au lieu de 8), et moins d'arrêts et de redémarrages du ventilateur. Ils reprenaient jusqu'ici les réglages de base, faits pour un PLA.
  - N-Soluble 111 : surplombs et ponts à 60 % au lieu de 100 %.
  - N-Soluble 150 : surplombs et ponts à 20 % au lieu de 100 %.
- **Vitesse de rétraction et de dérétraction** (ANA, ANA 300G et Lucy ; les EVA restent à 30 mm/s) : 35 mm/s au lieu de 30 mm/s.
- **Distance d'essuyage** (toutes les machines) : N-PLA, N-PVA, N-EASY FOOD, N-EASY V0, N-ABS, N-ABS-INDUS, N-ASA, N-PETG, N-PAHT CF, N-PC et Granulé étaient à 0 mm, ce qui rendait l'essuyage inactif. Ils reprennent les 2 mm de `fdm_filament_common`, comme toutes les autres matières.
- **Rétraction** (ANA, ANA 300G et Lucy ; les EVA ne changent pas) : N-PLA, N-PVA, N-EASY FOOD, N-EASY V0, N-ABS, N-ABS-INDUS, N-ASA, N-PETG, N-PAHT CF et Granulé reprennent les réglages de la machine. La longueur passe à 0.8 mm (au lieu de 0.5 mm, ou 0.7 mm pour PLA, PVA et EASY), et le saut en Z est de 0.4 mm en Normal Lift (au lieu de Slope Lift).
- **Températures de buse** (première couche et couches suivantes identiques) :
  - N-ABS : 280 °C (au lieu de 255).
  - N-ABS-INDUS : 270 °C (au lieu de 255, hérité de l'ABS).
  - N-PLA et N-PLX : 220 °C, plage 200-240 °C (le PLA était à 190-230 °C).
  - N-PETG-CF : 260 °C (au lieu de 255), plage 240-270 °C inchangée.
  - N-PETG-GF : 265 °C (au lieu de 260), plage 250-275 °C (au lieu de 250-270).
  - N-PPA CF : 300 °C (au lieu de 290).
  - N-PPS CF : 320 °C (au lieu de 330).
  - N-PC : 330 °C (au lieu de 280), plage 310-350 °C (au lieu de 270-290).

### Corrections
- **Nettoyage** : 20 clés inconnues d'OrcaSlicer (reprises de Bambu Studio) retirées de `fdm_filament_common`, ainsi que la clé `version` de `fdm_process_common`. Aucun effet sur les réglages.

### Installation / à savoir
- **Mise à jour** (version `01.01.02.00`) : même procédure que pour la version 01.01.00.00 (voir ci-dessous). Le changement de version déclenche la réinstallation automatique au démarrage.

## 09/10/2026 — version 01.01.01.00

Bundle : `Namma 09_10_2026.zip` (`Namma.json` + `Namma/`). Il remplace `Namma 06_10_2026.zip`.

### Corrections
- **Plantage de l'écran de sélection des imprimantes** (« type must be string, but is null ») : `nozzle_diameter` est rétabli dans les 8 variantes buse 0.4 (ANA 300, ANA 300 V2, ANA 300 HT, ANA 300G, ANA 600, Lucy 300, EVA 500 / 1000 - 3DF05). L'allègement du 06/10 l'avait retiré, alors qu'OrcaSlicer lit cette clé sans suivre l'héritage.

### Installation / à savoir
- **Mise à jour** (version `01.01.01.00`) : même procédure que pour la version 01.01.00.00 (voir ci-dessous). Le changement de version déclenche la réinstallation automatique au démarrage, y compris pour les postes qui ont déjà installé le bundle du 06/10.

## 06/10/2026 — version 01.01.00.00 (modifications du 02/10 au 06/10/2026)

Bundle : `Namma 06_10_2026.zip` (`Namma.json` + `Namma/`).

> Profils testés avec OrcaSlicer **2.4.2**. Le paramètre `chamber_minimal_temperature` utilisé dans le start G-code nécessite **OrcaSlicer 2.4.1 minimum**.

### Nouveautés

#### Machines
- **Namma ANA 300G** (buses 0.4 / 0.6 / 0.8) : la tête 1 utilise du filament, la tête 2 des granulés. Elle reprend la base de l'ANA 300, sans mode Copie / Miroir. La vignette est fournie.
- **Namma ANA 300 HT 0.8 nozzle** : les 3 profils process (0.24 Quality, 0.32 Standard, 0.32 Strength) et les 24 filaments HT qui la ciblaient deviennent utilisables.
- **Namma ANA 600 1.0 nozzle** : elle est désormais déclarée et chargée. Elle hérite de `fdm_ana_common` (2 têtes, G-code ANA), comme les autres ANA 600.

#### Filaments
- **Namma Granulé** (ANA 300G, buses 0.4 / 0.6 / 0.8), sur base PETG : flow 0.7, débit max 15 mm³/s, pressure advance 0.04, buse 240 °C (plage recommandée 190 à 275 °C), retrait XY 100 % (aucune compensation). C'est le filament par défaut de la tête 2.
- **Namma N-Soluble 90 / 111 / 150**, en remplacement de N-Soluble :

  | Profil | Buse | Ventilation | Plateau | Chambre |
  |---|---|---|---|---|
  | N-Soluble 90 | 230 °C | 80 % | 70 °C | — |
  | N-Soluble 111 | 240 °C | 40 % | 95 °C | 60 °C |
  | N-Soluble 150 | 285 °C | 10 % | 110 °C | 65 °C (90 °C sur ANA 300 HT) |

- **Profils 0.8 nozzle dédiés** pour les 20 matières de l'ANA 300, partagés avec l'ANA 300G 0.8 et la Lucy 300 0.8.
- **Une couleur par matière** (`default_filament_colour`), appliquée quand on choisit un filament. Les deux têtes des machines IDEX ont aussi des couleurs d'extrudeur différentes.

### Modifications

#### Process (toutes machines)
- **Jupe et bordure** : `skirt_loops` à 0, `brim_type` à `no_brim`.
- **Largeurs de ligne en % de la buse**, définies une seule fois dans `fdm_process_common` :

  | Ligne | Largeur |
  |---|---|
  | Default | 112.5 % |
  | First layer | 125 % |
  | Outer wall | = Default |
  | **Inner wall** | **125 %** |
  | Top surface | 80 % (100 % pour les EVA 0.96 / 2.00 / 2.40 mm) |
  | Sparse infill | 125 % |
  | Internal solid infill | 120 % |
  | Support / Bridge | 100 % |

- **Remplissage** : motif par défaut **Cubic** au lieu de Grid, et `minimum_sparse_infill_area` à 70 mm².
- **Épaisseur minimale du dessus et du fond** : 1 mm (Quality / Standard / Speed) et 1.5 mm (Strength).
- **Ponts** : `bridge_flow` et `internal_bridge_flow` à 1.35 sur tous les profils.
- **Supports activés par défaut** :

  | Réglage | Valeur |
  |---|---|
  | Type | Tree (auto) |
  | Style | Tree Hybrid |
  | Angle seuil | 40° |
  | Densité première couche | 100 % |
  | Parois de support | 1 |
  | Espacement du motif de base | 4 mm |
  | Interface | Rectilinear interlaced, espacement 0.25 mm |
  | Expansion | 2 mm |
  | Distance XY à l'objet | 0.5 mm |
  | Écart en première couche | 0.4 mm |

- **Tour de purge** : Prime volume à 40 mm³ au lieu de 100, Extra flow for purging à 150 % au lieu de 100 %.

#### Filaments
- **Température de chambre** (`chamber_minimal_temperature` = `chamber_temperature`), limitée à 65 °C, ou 90 °C sur l'ANA 300 HT :

  | Matière | Autres machines | ANA 300 HT |
  |---|---|---|
  | ABS, ABS-INDUS, ASA | 65 °C | 65 °C |
  | PC | 65 °C | 80 °C |
  | PPA CF | 65 °C | 80 °C |
  | PPS CF | 65 °C | 90 °C |
  | PAHT CF | 60 °C | 60 °C |
  | PEEK, PEI | — | 90 °C |
  | Autres matières | 0 | 0 |

  `activate_chamber_temp_control` est à 0 : la chambre est gérée par la macro de démarrage, sans `M191` d'OrcaSlicer.
- **BVOH, PVA, Soluble** : « Matériau soluble » et « Filament de support » sont cochés.
- **PEEK, PEI** : ventilation de 10 à 40 %, vitesse d'impression minimale 5 mm/s.
- **Tous les filaments** : « Don't slow down outer walls » est activé.
- **Max volumetric speed (ANA / Lucy)**, adapté à la Mosquito, à l'extrudeur LGX Pro et à une buse en acier trempé :

  | Matières | Débit |
  |---|---|
  | PLA, PLX, ABS, ABS-INDUS, ASA, PETG, PETG-CF / GF / GF UV / ESD, EASY FOOD, EASY V0 | 20 mm³/s |
  | PC, PAHT CF, PPA CF, PPS CF, PEEK, PEI | 10 mm³/s |
  | PVA, BVOH, Soluble 90 / 111 / 150 | 15 mm³/s |
  | TPU | 3 / 4 / 5 mm³/s en buse 0.4 / 0.6 / 0.8 |

  La valeur par défaut de `fdm_filament_common` passe de 5 à 20 mm³/s. Les EVA 3DF05 héritent des mêmes valeurs, sauf le TPU qui reste à 3.5. Les EVA grosses buses gardent 75.

#### Machines / G-code
- **Limites de hauteur de couche** : le minimum est à 0.08 mm sur toutes les machines. Il était à 0.016 ou 0.024 mm sur les buses autres que 0.4, ce qui n'est pas imprimable. Le maximum en buse 0.4 passe de 0.30 à 0.32 mm. Les autres buses restent à 80 % de leur diamètre.
- **Start G-code ANA et Lucy** : le paramètre `C` (température minimale de chambre) est passé à `start_print_ANA.g` / `start_print_Lucy.g`. Sur les ANA, c'est le maximum des têtes **réellement utilisées** dans l'impression.
- **Modes Copie / Miroir (ANA 300, ANA 300 V2)** : `X` / `Y` (coin minimum de la première couche) sont passés à la macro pour la ligne de purge.
- **End G-code EVA** : extinction du plateau et de la chauffe de chambre en fin d'impression.
- **Filaments par défaut** :
  - ANA 300 HT : N-ABS + **N-ASA** ;
  - ANA 300G : N-ABS + Granulé ;
  - `default_materials` des modèles couvre maintenant toutes les buses. Les profils par défaut sont ainsi cochés à la configuration et ne sont plus remplacés par Generic PLA / ABS.

### Corrections
- **Identifiants uniques** : nouveaux `setting_id` pour l'ANA 300 0.8 (`NMANA30008`), l'ANA 300 HT 0.4 / 0.6 (`NMANA300HT04/06`) et les EVA 500 (`NMEVA500…`). Nouveaux `model_id` des EVA 500 (`EVA500…`), qui étaient partagés avec les EVA 1000.
- **Buse en acier trempé** (`hardened_steel`) déclarée sur toutes les machines, au lieu du laiton.
- **Températures de ramollissement** : TPU à 60 °C (la valeur était vide), N-Soluble 90 / 111 / 150 à 90 / 111 / 150 °C (au lieu de 203).
- **N-PPS CF** : plage de buse recommandée jusqu'à 350 °C (elle s'arrêtait à 320 alors que la buse est à 330), et type renommé `PPS-CF`.
- **N-ASA** : ventilation de 15 à 50 % alignée sur l'ABS (elle était à 0 %).
- **Nettoyage** : suppression de 4 bases jamais utilisées (`fdm_process_common_lucy_ana`, `fdm_process_single_0.20`, `fdm_process_single_0.40_nozzle_0.8`, `fdm_machine_common`).
- **Bases machine** : `nozzle_diameter` contient une valeur par extrudeur (ANA / EVA : 2, Lucy : 1). Avant, il contenait la liste des buses, ce qui décrivait une machine à 3 ou 5 têtes.
- **ANA 600 1.0** : `nozzle_diameter` était mal formé (`"1.0,1.0"`), le filament par défaut `Generic PLA @System` était inexistant, et il manquait la hauteur de couche max (0.8) et le profil process par défaut.
- **Lucy 300 0.8** : elle n'avait aucun filament compatible. Elle partage maintenant les filaments ANA 300 0.8.
- **EVA 0.96 / 2.00 / 2.40 mm** : correction des erreurs de découpage « Too small line width » et `Flow::with_spacing()`, avec le dessus à 100 %.
- **Clé invalide** `chamber_minimal_temperatures` dans `fdm_filament_common` : remplacée par les clés correctes.
- **Allègement des profils** : 1 564 lignes qui répétaient la valeur héritée sont supprimées (`filament_vendor`, `enable_pressure_advance`, vitesses…). 23 valeurs communes à tous les enfants d'une base sont remontées dans la base. Le total passe de 9 856 à 8 144 lignes (-17 %), et la configuration effective des 567 profils sélectionnables est strictement identique.
- **Formatage** : tous les JSON passent à une ligne par paramètre, en UTF-8 sans BOM. Le contenu est inchangé.

### Installation / à savoir
- **Installation / mise à jour** (version `01.01.00.00`) : OrcaSlicer fermé, dézipper le bundle et copier `Namma.json` et le dossier `Namma/` dans `C:\Program Files\OrcaSlicer\resources\profiles\` (droits administrateur, remplacer les fichiers existants). Au démarrage suivant, OrcaSlicer installe automatiquement la nouvelle version. Ensuite, *Aide → Assistant de configuration* pour cocher les machines, buses et filaments voulus.
- **Points en attente de tests** (pression d'avance, flow ratio…) : voir `A_tester.md`.
- **Vignettes** : elles sont fournies dans le dossier `Namma/` et s'installent avec lui.
- **Première sélection d'une machine** : OrcaSlicer peut proposer *Generic PLA* sur la tête 1. Choisir le filament Namma une fois ; il est ensuite mémorisé.
- **Granulé** : OrcaSlicer ne peut pas réserver un filament à une seule tête. Sur l'ANA 300G, il faut choisir Granulé sur la tête 2.
