# Changelog — Profils Namma OrcaSlicer

## 05/10/2026 (modifications du 02/10 au 05/10/2026)

> Profils testés avec OrcaSlicer **2.4.2**. Le paramètre `chamber_minimal_temperature` utilisé dans le start G-code nécessite **OrcaSlicer 2.4.1 minimum**.

### Nouveautés

#### Machines
- **Namma ANA 300G** (buses 0.4 / 0.6 / 0.8) : la tête 1 utilise du filament, la tête 2 des granulés. Elle reprend la base de l'ANA 300, sans mode Copie / Miroir. La vignette est fournie.
- **Namma ANA 300 HT 0.8 nozzle** : les 3 profils process (0.24 Quality, 0.32 Standard, 0.32 Strength) et les 24 filaments HT qui la ciblaient deviennent utilisables.
- **Namma ANA 600 1.0 nozzle** : elle est désormais déclarée et chargée. Elle hérite de `fdm_ana_common` (2 têtes, G-code ANA), comme les autres ANA 600.

#### Filaments
- **Namma Granulé** (ANA 300G, buses 0.4 / 0.6 / 0.8), sur base PETG : flow 0.7, débit max 15 mm³/s, pressure advance 0.04. C'est le filament par défaut de la tête 2.
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

#### Machines / G-code
- **Start G-code ANA et Lucy** : le paramètre `C` (température minimale de chambre) est passé à `start_print_ANA.g` / `start_print_Lucy.g`. Sur les ANA, c'est le maximum des têtes **réellement utilisées** dans l'impression.
- **Modes Copie / Miroir (ANA 300, ANA 300 V2)** : `X` / `Y` (coin minimum de la première couche) sont passés à la macro pour la ligne de purge.
- **End G-code EVA** : extinction du plateau et de la chauffe de chambre en fin d'impression.
- **Filaments par défaut** :
  - ANA 300 HT : N-ABS + **N-ASA** ;
  - ANA 300G : N-ABS + Granulé ;
  - `default_materials` des modèles couvre maintenant toutes les buses. Les profils par défaut sont ainsi cochés à la configuration et ne sont plus remplacés par Generic PLA / ABS.

### Corrections
- **ANA 600 1.0** : `nozzle_diameter` était mal formé (`"1.0,1.0"`), le filament par défaut `Generic PLA @System` était inexistant, et il manquait la hauteur de couche max (0.8) et le profil process par défaut.
- **Lucy 300 0.8** : elle n'avait aucun filament compatible. Elle partage maintenant les filaments ANA 300 0.8.
- **EVA 0.96 / 2.00 / 2.40 mm** : correction des erreurs de découpage « Too small line width » et `Flow::with_spacing()`, avec le dessus à 100 %.
- **Clé invalide** `chamber_minimal_temperatures` dans `fdm_filament_common` : remplacée par les clés correctes.
- **Formatage** : tous les JSON passent à une ligne par paramètre, en UTF-8 sans BOM. Le contenu est inchangé.

### Installation / à savoir
- **Vignettes** : OrcaSlicer ne lit l'image de la barre latérale que dans `<installation OrcaSlicer>\resources\profiles\Namma\`. Il faut y copier les `*_cover.png`, avec les droits administrateur.
- **Première sélection d'une machine** : OrcaSlicer peut proposer *Generic PLA* sur la tête 1. Choisir le filament Namma une fois ; il est ensuite mémorisé.
- **Granulé** : OrcaSlicer ne peut pas réserver un filament à une seule tête. Sur l'ANA 300G, il faut choisir Granulé sur la tête 2.
