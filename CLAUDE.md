# CLAUDE.md — Slicer_Configuration (Namma)

Profils OrcaSlicer des imprimantes 3D **Namma** (gammes ANA, Lucy, EVA).
**Seul le dossier `OrcaSlicer/` est utilisé** : ne pas toucher aux autres dossiers du dépôt. Il n'y a pas de code applicatif, uniquement des profils JSON. La documentation et les messages de commit sont en **français**.

## Contexte

- `OrcaSlicer/Namma.json` : index du bundle vendor. `OrcaSlicer/Namma/` : tous les profils.
- `OrcaSlicer/Namma <JJ_MM_AAAA>[_vN].zip` : bundle livrable (contient `Namma.json` + `Namma/`), à régénérer à partir des fichiers à chaque release.
- `OrcaSlicer/Namma_Resume.md` : liste des machines et des filaments pour les utilisateurs.
- `OrcaSlicer/Changelog.md` : journal des changements, avec une section datée par livraison (Nouveautés / Modifications / Corrections / Installation). Le compléter à chaque série de changements.

## Arborescence OrcaSlicer

```
OrcaSlicer/
├── Namma.json                 # index : machine_model_list, machine_list, process_list, filament_list
└── Namma/
    ├── <Modèle>_cover.png     # vignette, nom = nom exact du machine_model + "_cover.png"
    ├── machine/               # machine_model + variantes par buse + fdm_*_common
    ├── process/               # profils d'impression + fdm_process_*
    └── filament/              # profils filament + fdm_filament_*
```

## Règles générales des fichiers JSON

1. **Le nom de fichier est égal au champ `name`** (`<name>.json`). Seule exception existante : les variantes `copy` / `miror` des ANA 300 (voir plus bas).
2. **Tout fichier ajouté, renommé ou supprimé doit être répercuté dans `Namma.json`** (entrée `{ "name", "sub_path" }` dans la bonne liste). Un profil absent de l'index n'est pas chargé par OrcaSlicer.
3. Un parent (`inherits`) doit être déclaré dans l'index **avant** ses enfants : les `fdm_*_common` en tête de liste, puis les intermédiaires, puis les profils finaux.
4. Champs d'en-tête, dans cet ordre : `type`, `name`, `inherits`, `from`, (`setting_id` / `filament_id`), `instantiation`.
   - `from` vaut toujours `"system"`.
   - `instantiation` vaut `"false"` pour les profils de base `fdm_*` (non visibles) et `"true"` pour les profils sélectionnables.
5. Valeurs : **toujours des chaînes** (`"0.4"`, `"1"`, `"50%"`), y compris les nombres et les booléens (`"0"`/`"1"`).
   - Les paramètres par extrudeur ou par filament sont des **tableaux** (`["0.95"]`). Pour les machines à 2 extrudeurs (ANA), il faut 2 valeurs (`["1500", "1500"]`).
   - `"nil"` signifie « hériter de la valeur machine » (champs `filament_retract_*`, `filament_wipe`, …).
6. **Ne surcharger que les clés qui diffèrent du parent** : les profils finaux restent courts. Les valeurs communes vont dans le `fdm_*` parent.
7. **Format : une ligne par variable.** Les tableaux de valeurs tiennent sur la ligne de leur clé (`"nozzle_diameter": ["0.4", "0.4"],`). Dans `Namma.json`, chaque entrée tient sur une ligne (`{ "name": "...", "sub_path": "..." },`). Indentation 2 espaces, UTF-8 **sans BOM**, pas de lignes vides. Fins de ligne : LF dans le dépôt (Git les convertit en CRLF sur Windows via `core.autocrlf`).
8. JSON strict : pas de virgule finale, pas de commentaires. Valider le JSON avant chaque commit.

## Machines (`machine/`)

### Hiérarchie
```
fdm_machine_common
fdm_ana_common   ─┐
fdm_lucy_common  ─┼─> "<Modèle> <buse> nozzle" (type machine, instantiation true)
fdm_eva_common   ─┘        └─> variantes "- Mode Copie" / "- Mode Miroir" (ANA 300, ANA 300 V2)
"<Modèle>.json"  = type "machine_model" (fiche modèle, pas d'héritage)
```

### Nommage
| Gamme | machine_model | machine (variante buse) |
|---|---|---|
| ANA / Lucy | `Namma ANA 300`, `Namma ANA 300 V2`, `Namma ANA 300 HT`, `Namma ANA 300G`, `Namma ANA 600`, `Namma Lucy 300` | `Namma ANA 300 0.4 nozzle` |
| EVA | `Namma EVA <500\|1000> - <tête>` (têtes `3DF05`, `3DF09`, `3DP25`) | `Namma EVA 500 - 3DF09 - 1.2 nozzle` (séparateur ` - `) |
| Modes IDEX (ANA) | — | `Namma ANA 300 0.4 nozzle - Mode Copie` / `- Mode Miroir` (fichiers `... nozzle copy.json` / `... nozzle miror.json`) |

### `machine_model`
Les champs sont `type: "machine_model"`, `name`, `model_id`, `nozzle_diameter` (liste séparée par `;`, ex. `"0.4;0.6;0.8"`), `family` (`ANA` / `Lucy` / `EVA`), `machine_tech: "FFF"`, `bed_model`, `bed_texture` et `default_materials` (noms de filaments séparés par `;`).
- **`default_materials` doit contenir les `default_filament_profile` de toutes les buses du modèle.** OrcaSlicer ne coche dans la liste des filaments visibles que les filaments listés ici. Un profil par défaut non visible est remplacé par `Generic PLA` / `Generic ABS @System`.

### Variante machine (buse)
- Champs obligatoires : `inherits` (le `fdm_<gamme>_common`), `setting_id`, `printer_model` (= nom du `machine_model`), `printer_variant` (= diamètre de buse), `nozzle_diameter`, `printable_area`, `default_filament_profile`, `default_print_profile`, `nozzle_type`.
- **`setting_id`** : `NM` + gamme + modèle + buse sur 2 chiffres + suffixe éventuel.
  - `NMANA30004` (ANA 300, buse 0.4), `NMANA30204` (ANA 300 V2), `NMANA60010` (ANA 600, buse 1.0), `NMLUCY30008`
  - `NMEVA10003DF0912` (EVA, tête 3DF09, buse 1.2), `NMEVA10003DP2530`
  - suffixe `C` = Mode Copie, `M` = Mode Miroir.
  - Le `setting_id` doit être **unique** (voir anomalies).
- `printable_area` : 4 coins `"XxY"` (ex. `["0x0","300x0","300x300","0x300"]`). En Mode Copie/Miroir, la largeur est réduite à environ la moitié (`145`).
- Firmware : **RepRapFirmware** (`gcode_flavor: "reprapfirmware"`). Le G-code (start/end/pause/changement de couche/changement de filament) se définit dans les `fdm_*_common`. Seuls les modes Copie/Miroir surchargent `machine_start_gcode`.
  - Le start G-code appelle les macros de la carte : `M98 P"0:/sys/start_print_ANA.g" T[current_extruder]` (ANA), `start_print.g` (EVA/Lucy). Le Mode Copie passe `T2` et le Mode Miroir `T3`.
  - Les températures sont réglées par `G10 P<outil> S{nozzle_temperature[i]}`, sous condition `is_extruder_used[i]`.
  - Placeholders OrcaSlicer : `[var]` et `{expr}`. Dans le JSON, échapper `"` en `\"` et les retours à la ligne en `\n`.
- **ANA 300G** : la tête 1 utilise du filament et la tête 2 des granulés. Il n'y a pas de mode Copie/Miroir. Le profil `Namma Granulé @Namma ANA 300G[ <buse> nozzle]` (base `fdm_filament_petg`) est le 2ᵉ élément de `default_filament_profile`. OrcaSlicer ne peut pas restreindre un filament à un seul extrudeur : les filaments ANA 300 restent sélectionnables sur les deux têtes.
- Filament EVA 3DF09/3DP25 : diamètre **2.85 mm** (3DP25 = granulés). Les autres machines utilisent 1.75 mm.

## Process (`process/`)

- **Nom** : `<hauteur de couche>mm <Qualité> @Namma <Modèle> <buse> nozzle`
  - hauteur sur 2 décimales (`0.20mm`, `2.40mm`)
  - qualité parmi `Quality`, `Standard`, `Strength`, `Speed`
  - Attention : pour l'EVA, le modèle est **sans la tête** (`0.60mm Standard @Namma EVA 500 1.2 nozzle`), et pour l'ANA 300 V2 avec espace (`@Namma ANA 300 V2 0.4 nozzle`).
- **Hiérarchie** :
  - `fdm_process_common` : base générale
  - `fdm_process_common_2` : base EVA grosses buses
  - `fdm_process_common_lucy_ana`
  - `fdm_process_single_<couche>[_nozzle_<buse>]` : intermédiaires par couche/buse (ex. `fdm_process_single_0.24_nozzle_0.6`)
  - le profil final hérite de l'intermédiaire adapté (ou directement d'un common).
- **Largeurs de ligne** : elles sont définies **uniquement** dans `fdm_process_common`, en % du diamètre de buse : Default 112.5 %, First layer 125 %, Outer wall `0` (= Default), Inner wall 125 %, Top surface 80 %, Sparse infill 125 %, Internal solid infill 120 %, Support 100 %, Bridge 100 %. Ne pas les redéfinir dans les intermédiaires ni dans les profils finaux.
  - **Exception** : OrcaSlicer refuse une largeur ≤ hauteur de couche (« Too small line width »). Au découpage, il refuse aussi une ligne qui devient plus étroite que la couche quand il resserre l'écartement (`Flow::with_spacing()`). Les profils EVA dont la couche vaut 80 % de la buse (`0.96mm Speed` 1.2, `2.00mm Speed` 2.5, `2.40mm Standard` 3.0, EVA 500 et 1000) surchargent donc `top_surface_line_width` à `100%`. Toute largeur doit rester ≥ 1.25 × la hauteur de couche.
- `compatible_printers` : liste **exacte** des noms de machines (variantes buse, plus Mode Copie/Miroir le cas échéant).
- Le profil référencé par `default_print_profile` d'une machine doit exister.
- Pour une nouvelle machine, créer la série complète des process pour chaque buse (même jeu que les modèles équivalents).

## Filaments (`filament/`)

- **Nom** : `Namma N-<MATIÈRE> @Namma <Modèle>[ <buse> nozzle]`
  - matières : `N-PLA`, `N-PLX`, `N-ABS`, `N-ABS-INDUS`, `N-ASA`, `N-PETG`, `N-PETG-CF`, `N-PETG-GF`, `N-PETG-GF UV`, `N-PETG-ESD`, `N-PC`, `N-TPU`, `N-PAHT CF`, `N-PPA CF`, `N-PPS CF`, `N-PEEK`, `N-PEI`, `N-BVOH`, `N-PVA`, `N-Soluble 90`, `N-Soluble 111`, `N-Soluble 150`, `N-EASY FOOD`, `N-EASY V0`.
  - ⚠️ Côté filament, les modèles s'écrivent **collés** : `ANA 300V2` et `ANA 300HT`, alors que les machines utilisent `ANA 300 V2` et `ANA 300 HT`. Conserver cette convention pour rester cohérent avec l'existant. Le lien réel se fait par `compatible_printers`.
  - EVA : nom complet avec la tête (`@Namma EVA 500 - 3DF09 - 1.2 nozzle`).
- **Hiérarchie** :
  ```
  fdm_filament_common                    (GFLA001)
   └─ fdm_filament_<matière>             (propriétés matière : type, densité, températures, ventilation, retraction…)
       └─ Namma N-X @Namma <Modèle>      (profil « modèle », sert souvent de base buse 0.8)
           └─ Namma N-X @Namma <Modèle> <buse> nozzle   (flow, PA, compatible_printers)
  ```
  Les filaments EVA héritent directement de `fdm_filament_<matière>`.
  Les solubles ont un niveau de plus : `fdm_filament_soluble` (propriétés communes, soluble et support) → `fdm_filament_soluble_<90|111|150>` (buse, ventilation, plateau, chambre) → profils `Namma N-Soluble <90|111|150> @...`.
  Pour l'ANA 300 (partagée avec la G) et le Granulé, le profil « modèle » est une base masquée (`instantiation: "false"`) : chaque buse, 0.8 comprise, a son propre profil `... <buse> nozzle`. Les autres gammes utilisent encore le profil « modèle » comme profil 0.8.
- `fdm_filament_<matière>` : `filament_vendor: ["Namma"]`, `filament_type`, `filament_id` (`GFLAxxx`), températures, `filament_max_volumetric_speed`, etc.
- Profil final : `filament_id` = `name`, `filament_vendor: ["Namma"]`, puis les surcharges spécifiques (`pressure_advance`, `enable_pressure_advance`, `filament_flow_ratio`, `filament_max_volumetric_speed`, `filament_diameter` pour l'EVA) et `compatible_printers`.
- Un filament ANA 300 0.4 est aussi déclaré compatible avec `Namma Lucy 300 0.4 nozzle` et avec les modes Copie/Miroir. Penser à ces variantes lors d'un ajout.
- **Couleurs** : chaque `fdm_filament_<matière>` a sa propre `default_filament_colour`. N-ABS-INDUS a la sienne (`#B71C1C`), posée sur ses profils qui héritent de `fdm_filament_abs`, et le Granulé aussi (`#FF6D00`). Une nouvelle matière doit avoir une couleur distincte des autres. OrcaSlicer n'applique cette couleur que quand on choisit le filament à la main. Sinon, il reprend la couleur mémorisée pour l'imprimante, ou `#26A69A` par défaut.
- Machines à 2 têtes (ANA via `fdm_ana_common`, EVA 3DF05) : `extruder_colour` vaut `["#018001", "#FF6D00"]`.
- Pour une nouvelle matière : créer `fdm_filament_<matière>.json`, puis un fichier par modèle et par buse, puis les entrées dans `filament_list` de `Namma.json`. Mettre à jour `Namma_Resume.md`.

## Ajouter une machine — checklist

1. `machine/<Modèle>.json` (machine_model) avec un `model_id` unique.
2. `machine/<Modèle> <buse> nozzle.json` pour chaque buse, avec un `setting_id` unique.
3. `Namma/<Modèle>_cover.png`.
4. Process pour chaque buse, avec `compatible_printers` à jour.
5. Filaments : nouveaux fichiers, ou ajout du nom de machine dans `compatible_printers` des existants.
6. `Namma.json` : toutes les entrées (le machine_model dans `machine_model_list`, les variantes dans `machine_list`).
7. `Namma_Resume.md`.
8. Vérifier que les noms référencés (`inherits`, `compatible_printers`, `default_*_profile`, `default_materials`) existent.

## Release

- Zipper `Namma.json` + `Namma/` sous `OrcaSlicer/Namma <JJ_MM_AAAA>[_vN].zip`. Ce zip est ensuite importé dans OrcaSlicer.
- Vignettes : l'image de la barre latérale d'OrcaSlicer (`Sidebar::update_printer_thumbnail`) est cherchée **uniquement** dans `<dossier d'installation OrcaSlicer>/resources/profiles/Namma/<printer_model>_cover.png`, pas dans `%APPDATA%\OrcaSlicer\system\Namma\`. Pour un nouveau modèle, il faut copier le `_cover.png` dans ce dossier `resources`, sinon une icône générique s'affiche.
- Incrémenter `version` dans `Namma.json` (format `01.00.00.00`) quand le bundle change. Mettre `force_update` à `"1"` pour forcer la mise à jour chez les utilisateurs.

## Git

- Branche principale `main`. Les évolutions passent par des branches (ex. `EVA-500/1000`, `Test`) puis une PR.
- Messages de commit en français, courts et descriptifs (ex. `Modif 3DF09_3DP25`, `Rajout photo Ana 300G`).

## Anomalies connues (à corriger ou à ne pas reproduire)

- `setting_id` en double :
  - `Namma ANA 300 0.8 nozzle` = `NMANA30006` (devrait être `NMANA30008`)
  - `ANA 300 HT 0.4/0.6` = `NMANA30004/06` (identiques à l'ANA 300)
  - EVA 500 et EVA 1000 partagent tous leurs `setting_id` (`NMEVA1000…`) et leurs `model_id` (`EVA1000…`).
- `default_materials` des machine_model EVA pointent vers des filaments ANA 300.
- Non déclaré dans `Namma.json` : `process/fdm_process_single_0.40_nozzle_0.8.json`.- Faute de frappe historique `miror` dans les noms de fichiers. Ne pas renommer sans mettre à jour l'index.
