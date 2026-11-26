# MCD tables — dictionnaire des champs

Fichier de tables uniquement. Les relations sont dans `MCD-261116.md` ; les catalogues de valeurs dans `MCD Bibliothèques.md` ; les points à trancher dans `MCD-Questions.md`.

**Conventions** :
- `Obligatoire = Oui` : sans ce champ, la facturation serait juridiquement incomplète (GT #04 §7) — savoir **qui**, **quand**, **combien d'équipements**. Colonne vide = champ facultatif.
- `Clé` : `PK`, `FK`, `PK+FK` (jonction) ou vide.
- Les types sont indicatifs (préparation du passage au modèle logique).

## AODE

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | SIREN_AODE | PK | Identifiant de la structure AODE | — | Oui |
| string | Nom_AODE | — | Raison sociale de l'AODE | — | Oui |
| string | Adresse_siege | — | Adresse du siège | — | |
| string | commune_insee_siege | — | Code INSEE du siège | — | |
| string | Contact_nom | — | Contact référent | — | |
| string | Contact_email | — | Email de contact | — | |
| string | Contact_telephone | — | Téléphone de contact | — | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## GRD_E

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | SIREN_GRDE | PK | SIREN du gestionnaire de réseau électrique | — | Oui |
| string | Nom_GRDE | — | Raison sociale du GRD-E (ex. Enedis) | — | Oui |
| string | Adresse_siege | — | Adresse du siège | — | |
| string | Contact_nom | — | Contact référent | — | |
| string | Contact_email | — | Email de contact | — | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## Operateur

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | SIREN_operateur | PK | Identifiant opérateur télécom ou occupant tiers | — | Oui |
| string | Raison_sociale | — | Nom de l'opérateur | — | Oui |
| string | Statut_tier | — | Statut qualifiable (opérateur télécom, occupant tiers, autre) | — | Oui |
| string | Code_ARCEP | — | Numéro ARCEP | — | |
| string | Ref_prestataire | — | Prestataire terrain signalé dans les références d'affaire | — | |
| string | Adresse_siege | — | Adresse du siège | — | |
| string | commune_insee_siege | — | Code INSEE du siège | — | |
| string | Contact_nom | — | Contact référent | — | |
| string | Contact_email | — | Email de contact | — | |
| string | Contact_telephone | — | Téléphone de contact | — | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## Sous_traitant

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | SIREN_Intervenant | PK | Identifiant du sous-traitant | — | Oui |
| string | Raison_sociale | — | Nom du sous-traitant | — | Oui |
| string | Specialite | — | Prestation réalisée (relevé, installation…) | — | |
| string | Adresse_siege | — | Adresse du siège | — | |
| string | Contact_nom | — | Contact référent | — | |
| string | Contact_email | — | Email de contact | — | |
| date | Date_MAJ | — | Date de mise à jour | date | |

## Supports

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_support | PK | Identifiant unique du support — préfixe code INSEE (GT #04 §4) | — | Oui |
| int | SIREN_AODE | FK | Propriétaire AODE du support | — | Oui |
| int | SIREN_GRDE | FK | GRD-E gestionnaire du support | — | Oui |
| string | Ref_ENEDIS | — | Référence poteau Enedis (désambiguïsation des échanges) | — | |
| float | Longitude | — | Longitude WGS84 (arbitrage GT #04 §5 en cours) | degré décimal | |
| float | Latitude | — | Latitude WGS84 (arbitrage GT #04 §5 en cours) | degré décimal | |
| float | X | — | Coordonnée X projetée (convention Enedis annexe 8, RGF93) | m | Oui |
| float | Y | — | Coordonnée Y projetée | m | Oui |
| string | Projection | — | Système de projection | code EPSG | Oui |
| string | ClassePrecision | — | Précision du relevé | — | |
| string | commune_nom | — | Nom de commune | — | |
| string | commune_insee | — | Code INSEE (base du nommage) | — | Oui |
| string | adresse_support | — | Rue, numéro, complément | — | |
| string | Fabricant | — | Fabricant ou marque | — | |
| string | TypePhysique | — | Type de support | — | |
| string | Materiau | — | Matériau | — | |
| float | Hauteur_support | — | Hauteur du support | m | |
| string | Structure_support | — | Forme ou structure de l'appui | — | |
| boolean | BoisCreosote | — | Traitement ou protection du support (bois créosoté) | vrai/faux | |
| string | ClasseResistance | — | Classe de résistance | — | |
| float | EffortTransversal | — | Effort admissible | daN | |
| date | DateConstruction | — | Date de pose ou construction | date | |
| string | Etat_support | — | État du support | — | |
| string | Nature | — | Nature ou fonction d'usage | — | |
| boolean | Bandeau_vert | — | Présence du bandeau vert | vrai/faux | |
| boolean | Depose | — | Support déposé (exclut la facturation, GT #04 §6) | vrai/faux | Oui |
| date | Date_depose | — | Date de dépose si connue | date | |
| date | Date_MAJ | — | Date de mise à jour (trace le basculement) | date | Oui |

## Equipement_traverse

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_Eq_traverse | PK | Identifiant de la traverse | — | Oui |
| int | Ref_Id_support | FK | Support d'installation | — | Oui |
| int | SIREN_operateur | FK | Opérateur propriétaire | — | Oui |
| int | Ref_Id_Occupation | FK | Droit dont la traverse relève (0..1) | — | Oui |
| string | Type_traverse | — | Type de traverse | — | |
| string | Caracteristiques | — | Libellé, dimensions, capacité | — | |
| date | Date_installation | — | Date de pose | date | |

## Equipement_cable

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_Eq_cable | PK | Identifiant du câble | — | Oui |
| int | SIREN_operateur | FK | Opérateur propriétaire | — | Oui |
| string | Type_cable | — | Type de câble | — | |
| string | Caracteristiques_cable | — | Libellé, diamètre, capacité | mm (diamètre) | |
| date | Date_installation | — | Date de pose | date | |

## Equipement_autre

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_Eq_autre | PK | Identifiant de l'équipement autre (boîtier, IoT, caméra, miroir…) | — | Oui |
| int | Ref_Id_support | FK | Support d'installation | — | Oui |
| int | SIREN_operateur | FK | Opérateur propriétaire | — | Oui |
| string | Type_equipement | — | Boîtier fibre, IoT, capteur, caméra, miroir, éclairage public… | — | |
| string | Caracteristiques | — | Libellé, caractéristiques | — | |
| date | Date_installation | — | Date d'installation | date | |

## Parcours_cable

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Ref_Id_cable | PK+FK | Câble concerné | — | Oui |
| int | Ref_Id_traverse | PK+FK | Traverse franchie | — | Oui |
| int | Ordre | — | Position de la traverse dans le parcours | rang | |

## Perimetre_occupation

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Ref_Id_Occupation | PK+FK | Droit d'occupation | — | Oui |
| int | Ref_Id_support | PK+FK | Support concerné par le tronçon | — | Oui |

## Droit_Occupation

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_Occupation | PK | Identifiant de l'occupation (numéro arbitraire, GT #04 §4) | — | Oui |
| int | SIREN_operateur | FK | Opérateur bénéficiaire du droit (qui facturer) | — | Oui |
| int | SIREN_GRDE | FK | Exploitant électrique propriétaire du poteau | — | |
| string | Affaire | — | Référence de l'affaire | — | Oui |
| string | Ref_ENEDIS | — | Référence affaire Enedis | — | |
| string | Ref_affaire_operateur | — | Référence affaire opérateur | — | Oui |
| string | Ref_affaire_prestataire | — | Référence affaire du prestataire terrain | — | |
| string | Etat_affaire | — | État de l'affaire | — | Oui |
| string | Type_convention | — | Cadre réglementaire ou type de convention | — | |
| string | Ref_convention | — | Convention ou autorisation d'utilisation | — | Oui |
| boolean | Traverses_presentes | — | Traverses présentes (combien d'équipements) | vrai/faux | Oui |
| float | Taux_utilisation | — | Taux d'utilisation du support | % | |
| string | Etat_support_constate | — | État du support constaté | — | |
| date | Date_debut_occupation | — | Date de début d'occupation | date | Oui |
| int | Duree_occupation | — | Durée d'occupation | mois | |
| date | Date_depot_etude | — | Date de dépôt étude / AAT / Shape | date | |
| date | Date_validation_etude | — | Date de validation de l'étude | date | |
| date | Date_refus | — | Dates de refus | date | |
| string | AAT | — | Attestation d'appui technique (donnée qui compte pour la facturation, GT #04 §10) | — | |
| string | Photo_support | — | Photos (fichiers joints conservés en local) | chemin/URL | |
| string | Commentaires | — | Commentaires ou observations | — | |
| date | Date_MAJ | — | Date de mise à jour de la donnée | date | |

## Facturation

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_facture | PK | Identifiant de la facture | — | Oui |
| int | SIREN_AODE | FK | AODE émetteur | — | Oui |
| int | SIREN_operateur | FK | Opérateur facturé | — | Oui |
| int | Periode | — | Période de facturation | AAAA (ou AAAAMM, à trancher) | Oui |
| date | Date_emission | — | Date d'émission de la facture | date | |
| int | Annee_paiement | — | Année de paiement (traçabilité, GT #04 §3) | AAAA | Oui |
| int | Annee_prochaine_redevance | — | Prochaine redevance (option alerte, GT #04 §3) | AAAA | |
| string | Destinataire_service | — | Service financier destinataire (circuit de facturation) | — | |

## Ligne_facturation

| Type | Champ | Clé | Description | Unité | Obligatoire |
|---|---|---|---|---|---|
| int | Id_ligne | PK | Identifiant de ligne | — | Oui |
| int | Ref_Id_facture | FK | Facture alimentée par la ligne | — | Oui |
| int | Ref_Id_Occupation | FK | Droit facturé | — | Oui |
| int | Periode_facturee | — | Période d'occupation facturée | AAAA (ou AAAAMM, à trancher) | Oui |
| int | Montant | — | Montant facturé pour la période | € | Oui |

---

**Contraintes d'unicité à prévoir** :
- `Ligne_facturation` : couple (`Ref_Id_Occupation`, `Periode_facturee`) — un droit n'est facturé qu'une fois par période ;
- `Perimetre_occupation` et `Parcours_cable` : PK composites (déjà portées par les deux champs).
