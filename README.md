# MCD — Appuis Communs (FNCCR / France Data Réseau)

Modèle Conceptuel de Données pour le suivi des **appuis communs** (poteaux AODE) et des **droits d'occupation** des opérateurs de télécommunications.

## 📑 Sommaire

1. [Objet](#-objet)
2. [Organisation du dépôt](#-organisation-du-dépôt)
3. [Entités principales](#-entités-principales)
4. [Contribuer — suggérer des modifications](#-contribuer--suggérer-des-modifications)
5. [Feuille de route](#-feuille-de-route)
6. [Visualisation](#-visualisation)
7. [Glossaire](#-glossaire)
8. [Contact](#-contact)
9. [Licence](#-licence)

## 🎯 Objet

Ce MCD décrit le cycle de vie complet des supports partagés entre opérateurs :

- les **supports** (poteaux appartenant à des AODE, gérés par un GRD-E) ;
- les **équipements** qui y sont installés : traverses, câbles, équipements annexes ;
- les **droits d'occupation** (conventions autorisant l'installation de traverses sur un ou plusieurs supports — notion de tronçon) ;
- la **facturation** périodique des redevances d'utilisation aux opérateurs ;
- les **acteurs** : AODE, GRD-E, opérateurs télécom, sous-traitants.

Le cœur fonctionnel du modèle est la génération périodique, sur demande, des factures de redevance : chaque **ligne de facturation** lie un **droit d'occupation** à une **période**, et l'ensemble des lignes alimente une **facture** (une AODE émettrice, un opérateur facturé).

## 📁 Organisation du dépôt

```
fdr-appuiscommuns-v2/
├── README.md               → ce fichier
├── MCD/                    → fichiers du modèle conceptuel de données
│   ├── MCD Relations.md        → schéma de référence (liaisons entre tables)
│   ├── MCD Relations classDiag.md → même schéma, notation UML classDiagram
│   ├── MCD Tables.md           → dictionnaire des champs, table par table
│   ├── MCD Bibliothèques.md     → dictionnaire des catalogues de valeurs
│   └── MCD Questions.md        → points de vigilance et questions ouvertes
├── CSV Tables/             → un CSV par table du MCD (structure)
└── CSV Bibliothèques/      → un CSV par catalogue de valeurs (structure)
```

| Fichier / dossier | Description |
|---|---|
| `MCD/MCD Relations.md` | **Schéma de référence**, en syntaxe Mermaid `erDiagram` : tables relationnelles (PK, FK) et liaisons entre elles |
| `MCD/MCD Relations classDiag.md` | **Même schéma en notation UML** (`classDiagram`), pour les lecteurs familiers de cette notation |
| `MCD/MCD Tables.md` | **Dictionnaire des champs** : pour chaque table et chaque champ — type, nom, clé, description, unité, caractère obligatoire |
| `MCD/MCD Bibliothèques.md` | **Catalogues de valeurs** partagés (fabricants, matériaux, types de câbles…) pour fiabiliser la saisie par référence plutôt qu'en texte libre |
| `MCD/MCD Questions.md` | Points de vigilance et questions ouvertes à trancher collectivement |
| `CSV Tables/` | **Un fichier CSV par table** (13 fichiers : `Supports.csv`, `Droit_Occupation.csv`, `Facturation.csv`…), même format que le dictionnaire : `Type,Champ,Cle,Description,Unite,Obligatoire` |
| `CSV Bibliothèques/` | **Un fichier CSV par bibliothèque** (13 fichiers : `Bibliotheque_TypeCable.csv`, `Bibliotheque_Fabricant.csv`…) |

**Logique de rangement** :
* le dossier `MCD/` porte la **documentation lisible** (schéma et dictionnaires) ;
* les dossiers `CSV Tables/` et `CSV Bibliothèques/` en sont la **version exploitable machine** (Excel, scripts, validateur d'import), toujours synchronisée avec les `.md`.
Les deux existent car le GT #04 a acté la double diffusion : Markdown pour le partage collaboratif, CSV pour les AODE qui travaillent en tableur.

## 🧩 Entités principales

```text
AODE ──possède──> Supports <──gère── GRD_E
                     │
                     └──porte──> Equipement_traverse ──couvre── Droit_Occupation
                                    │                           │
                                    └──(Parcours_cable)── Equipement_cable
                                                                │
                                    Ligne_facturation <────────┘
                                           │
                                      Facturation
```

- **`Perimetre_occupation`** (association) : couple droit × support, matérialisant la notion de **tronçon** — un droit peut couvrir plusieurs supports ;
- **`Parcours_cable`** (association) : franchissement des traverses par les câbles (N:M) — information complémentaire d'inventaire, sans portée conventionnelle ;
- **`Facturation` / `Ligne_facturation`** : un droit × une période = une ligne ; un ensemble de lignes = une facture.

## 🤝 Contribuer — suggérer des modifications

Le MCD fait l'objet d'une **construction collective** : chaque AODE est invité à s'approprier le modèle et à transmettre ses remarques. Deux voies, au choix :

### 1. Modifier les fichiers `.md` directement

Ouvrez une **issue** décrivant la remarque (champ manquant, libellé à corriger, question sur une cardinalité…), ou proposez vous-même la modification via une **pull request** sur le fichier concerné (`MCD/MCD Tables.md`, `MCD/MCD Bibliothèques.md`, `MCD/MCD Relations.md`…). Les blocs Mermaid sont automatiquement rendus par GitHub, ce qui permet de visualiser le schéma modifié directement dans la PR.

### 2. Modifier les fichiers CSV

Pour les remarques portant sur un champ précis (description, unité, caractère obligatoire, ajout d'une valeur dans une bibliothèque), le plus simple est d'éditer le CSV concerné :

- directement **sur GitHub** (bouton *Edit* sur le fichier : GitHub ouvre un éditeur et crée automatiquement la pull request) ;
- ou en local : ouvrez le CSV dans un tableur, modifiez, enregistrez au format CSV (virgule séparateur, champs entre guillemets doubles), puis soumettez une pull request.

**Règles de cohérence** : toute modification doit être répercutée sur les deux supports (`.md` et CSV de la même table/bibliothèque) ; l'ajout d'une valeur dans un CSV de bibliothèque ne nécessite pas de changement du schéma ; l'ajout d'un champ ou d'une table doit être discuté en GT (référence à ouvrir dans `MCD/MCD Questions.md`).

## 🗺️ Feuille de route

1. Trancher les points listés dans `MCD/MCD Questions.md` (propriété du support, lien facturation/convention, coordonnées WGS84 vs RGF93, charte de nommage, table des tiers…) ;
2. Valider collectivement la revue champ par champ (obligatoire/facultatif, nommage, formats — GT #04 §7) et les bibliothèques communes (GT #04 §8) ;
3. Traduire le modèle en **GeoPackage** (SQLite) pour un usage SIG (QGIS) ; GML envisagé comme format d'échange.

## 🔧 Visualisation

Les fichiers `.md` contiennent des blocs de code Mermaid : ils sont rendus nativement par GitHub/GitLab, Obsidian (extension Mermaid), VS Code (extension Markdown Preview Mermaid Support), ou en ligne sur [mermaid.live](https://mermaid.live). Les fichiers CSV s'ouvrent dans tout tableur.

## 📖 Glossaire

| Terme | Signification |
|---|---|
| AODE | Autorité Organisatrice de la Distribution d'Électricité |
| GRD-E | Gestionnaire de Réseau de Distribution Électrique |
| Appui commun | Support (poteau) ouvert au partage entre opérateurs |
| Traverse / Bef | Équipement porteur installé sur le support |
| Droit d'occupation | Convention autorisant l'occupation d'appuis par un opérateur |
| PK / FK / UK | Clé primaire / clé étrangère / clé unique |

## 📮 Contact

- **Référente cas d'usage « Appuis communs »** : Mireille Bonnin (FNCCR)
- **Appui à la maîtrise d'ouvrage (AMO)** : Sylvain Fritsch (ALRIG Conseil)
- **Cadre de travail** : GT « Appuis communs » France Data Réseau.

## 📜 Licence

* Les travaux du GT Appuis Communs au sein de FDR sont réalisés sous Licence Ouverte Etalab 2.0
* https://www.data.gouv.fr/pages/legal/licences/etalab-2-0