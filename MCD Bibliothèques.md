# MCD Bibliothèques — catalogues de valeurs

Tables catalogues pour renseigner les champs descriptifs du MCD par référence plutôt qu'en saisie libre. Objectifs (GT #04 §7-8) : fiabiliser la saisie (listes déroulantes, notamment en CSV/tableur), partager les bibliothèques entre AODE, et faire évoluer les listes sans toucher au schéma.

**Conventions** : format identique à `MCD tables.md` — `Type | Champ | Clé | Description | Unité | Obligatoire`. Colonne Obligatoire vide = champ facultatif. Chaque bibliothèque suit le même patron : identifiant, libellé, complément(s) thématique(s), date de mise à jour.

## Bibliotheque_Fabricant

Renseigne `Supports.Fabricant`.

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_fabricant | PK | Identifiant fabricant | — | Oui |
| string | Nom_fabricant | — | Nom du fabricant ou de la marque | — | Oui |
| string | Pays | — | Pays d'origine | — | |
| string | Site_web | — | Site web | URL | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## Bibliotheque_Materiau

Renseigne `Supports.Materiau`.

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_materiau | PK | Identifiant matériau | — | Oui |
| string | Nom_materiau | — | Libellé du matériau (bois, béton, acier, composite…) | — | Oui |
| string | Description | — | Description, notes d'usage | — | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## Bibliotheque_TypeSupport

Renseigne `Supports.TypePhysique`.

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_type_support | PK | Identifiant du type de support | — | Oui |
| string | Libelle | — | Libellé du type (poteau BT, poteau HTA, façade, pyramide…) | — | Oui |
| string | Description | — | Description, cas d'usage | — | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## Bibliotheque_Structure

Renseigne `Supports.Structure_support`.

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_structure | PK | Identifiant de la forme ou structure d'appui | — | Oui |
| string | Libelle | — | Libellé (coffret, console, fut…) | — | Oui |
| string | Description | — | Description | — | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## Bibliotheque_ClassePrecision

Renseigne `Supports.ClassePrecision`.

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_classe_precision | PK | Identifiant de la classe de précision | — | Oui |
| string | Libelle | — | Libellé de la classe (GPS, cadastrale, adresse, approximative…) | — | Oui |
| string | Description | — | Précision théorique associée | — | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## Bibliotheque_Etat

Renseigne `Supports.Etat_support` et `Droit_Occupation.Etat_support_constate`.

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_etat | PK | Identifiant de l'état | — | Oui |
| string | Libelle | — | Libellé de l'état (neuf, bon, passable, dégradé, hors service, déposé…) | — | Oui |
| string | Description | — | Description, critères de constat | — | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## Bibliotheque_TypeTraverse

Renseigne `Equipement_traverse.Type_traverse`.

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_type_traverse | PK | Identifiant du type de traverse | — | Oui |
| string | Libelle | — | Libellé du type (bef, traverse métallique, goulotte…) | — | Oui |
| string | Caracteristiques | — | Dimensions et capacités standard | — | |
| int | Nb_cables_max | — | Nombre de câbles admissible | câbles | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## Bibliotheque_TypeCable

Renseigne `Equipement_cable.Type_cable`.

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_type_cable | PK | Identifiant du type de câble | — | Oui |
| string | Libelle | — | Libellé du type (fibre BOFO, fibre AOC, cuivre, coaxial…) | — | Oui |
| string | Fibre_type | — | Type de fibre (G.652, G.657…) | — | |
| int | Nombre_fibres | — | Capacité en fibres | fibres | |
| float | Diametre | — | Diamètre | mm | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## Bibliotheque_TypeEquipementAutre

Renseigne `Equipement_autre.Type_equipement`. Socle évolutif (GT #04 §2) : boîtiers fibre, IoT, vidéoprotection, capteurs, miroirs, éclairage public…

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_type_eq_autre | PK | Identifiant du type d'équipement autre | — | Oui |
| string | Libelle | — | Libellé (boîtier fibre PM, capteur IoT, capteur CO2, caméra, miroir, radar pédagogique, luminaire…) | — | Oui |
| string | Description | — | Description, cas d'usage | — | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## Bibliotheque_StatutTiers

Renseigne `Operateur.Statut_tier`. Statut qualifiable (GT #04 §7-8).

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_statut | PK | Identifiant du statut | — | Oui |
| string | Libelle | — | Libellé (opérateur télécom, occupant tiers, GRD-E, prestataire…) | — | Oui |
| string | Description | — | Définition du statut | — | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## Bibliotheque_TypeConvention

Renseigne `Droit_Occupation.Type_convention`.

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_type_convention | PK | Identifiant du type de convention | — | Oui |
| string | Libelle | — | Libellé (convention type 2015, AAT simplifiée, accord cadre…) | — | Oui |
| string | Cadre_reglementaire | — | Cadre réglementaire de référence (L.33, décret…) | — | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## Bibliotheque_EtatAffaire

Renseigne `Droit_Occupation.Etat_affaire`.

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_etat_affaire | PK | Identifiant de l'état d'affaire | — | Oui |
| string | Libelle | — | Libellé (déposée, validée, refusée, close…) | — | Oui |
| string | Description | — | Description de l'étape du cycle de vie | — | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## Bibliotheque_Prestation

Renseigne `Sous_traitant.Specialite`.

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_prestation | PK | Identifiant de la prestation | — | Oui |
| string | Libelle | — | Libellé (relevé terrain, installation, raccordement, étude, AAT…) | — | Oui |
| string | Description | — | Description de la prestation | — | |
| date | Date_MAJ | — | Date de mise à jour | date | |

---

## Mode d'emploi

Deux options d'intégration, à trancher lors du passage au modèle logique (cf. `MCD-Questions.md`, point 10) :

- **FK stricte** : remplacer le champ texte par un identifiant (ex. `int Id_materiau FK` dans Supports), ce qui garantit l'intégrité référentielle ;
- **Catalogue de contrôle** : conserver le texte dans la table, la bibliothèque servant de liste de contrôle — moins rigide, applicable dès maintenant, la FK stricte pouvant être mise en place progressivement.

La table de correspondance champ ↔ bibliothèque est rappelée en tête de chaque section (« Renseigne… »).
