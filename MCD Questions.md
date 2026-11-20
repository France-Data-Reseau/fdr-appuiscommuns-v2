## Points de vigilance

1. **Propriété du support** : un support peut-il avoir un autre propriétaire qu'un AODE (GRD-E, tiers) ? Si oui, `SIREN_AODE` devient optionnel et la cardinalité `AODE|o--o{Supports` (0,1)-(0,n).
2. **Lien Facturation / Convention** : la facture se fonde sur la convention AODE-Opérateur (N:M conceptuel, sans table). Faut-il créer l'entité `Convention` de redevance (avec tarif applicable) et relier `Facturation` à elle, ou rester au stade conceptuel ? (la ligne de tarification peut *simplement* mentionner la convention)
3. **Tables de jonction contractuelles** : les N:M `concède` (AODE-GRD_E) et sous-traitant/opérateur devront être résolus en tables de jonction au passage au modèle logique (GPKG) par l'ajout de tables intermédiaires (`Concession` ; `Intervention`)
4. **Unicité des lignes** : contrainte à prévoir sur le couple (`Ref_Id_Occupation`, `Periode_facturee`) dans `Ligne_facturation` — un droit n'est facturé qu'une fois par période.
5. **Format des coordonnées** (GT #04 §5) : longitude/latitude WGS84 à privilégier in fine vs X/Y projetées de la convention Enedis (RGF93) ; arbitrage collectif à confirmer. Les deux familles de champs sont présentes dans `Supports` en attendant.
6. **Format des périodes** : `Periode` / `Periode_facturee` à formater (AAAA ou AAAAMM ?), dans l'esprit de la revue champ par champ (GT #04 §7).
7. **Champs obligatoires** (GT #04 §7) : proposition `[O]`/`[F]` posée dans `MCD tables.md`, à valider champ par champ — rappel du GT : les champs « nécessaires » ne sont pas forcément connus (certains nécessaires difficiles à renseigner, certains facultatifs déjà disponibles) ; l'obligation n'est pas une obligation de remplissage.
8. **Nomming des supports** (GT #04 §4) : charte de nommage et règles d'unicité inter-AODE à définir collectivement (règle pratiquée : préfixe INSEE + suite sans doublon dans la commune) ; table de correspondance AODE ↔ Enedis envisageable.
9. **Supports déposés** (GT #04 §6) : champ booléen + date retenus comme minimum garanti ; option d'une table dédiée à trancher.
10. **Bibliothèques communes** (GT #04 §8, `MCD Bibliothèques.md`) : 13 tables catalogues candidates au partage entre AODE. À trancher : mode d'intégration (FK stricte vs catalogue de contrôle sur texte saisi), périmètre de partage et d'ouverture (bibliothèques publiques vs interne FNCCR), mode d'alimentation collaborative (validation centralisée vs proposition par chaque AODE), et statut de référence nationale vs locale (possibilité de surcharges locales).
11. **Table des tiers** (GT #04 §8) : structure à arbitrer — table tiers unique (AODE, opérateurs, Enedis, prestataires) ou tables séparées (actuellement AODE, GRD_E, Operateur, Sous_traitant distincts, avec `Statut_tier` qualifiable) ; impact sur les bibliothèques candidates au partage.

## Notes de construction (MCD tables)

- Structure issue de la discussion MCD du 19/11/2026 (tables relationnelles alignées sur `MCD-261116.md`), complétée par les apports du GT #04 du 15/10/2026 (`Ref_ENEDIS`, longitude/latitude, `Depose`, `Annee_paiement`, `Statut_tier`, `AAT`, nommage par préfixe INSEE), puis par les champs descriptifs de la matrice Excel.
- Le fichier liste les **tables uniquement** (une table par entité, tous champs confondus). Un combo « tables détaillées + liaisons relationnelles » est prévu ultérieurement.
- En base physique (GeoPackage), chaque table serait une vraie table ; les bibliothèques communes candidates au partage entre AODE sont `Operateur` et `Sous_traitant` (GT #04 §8).

