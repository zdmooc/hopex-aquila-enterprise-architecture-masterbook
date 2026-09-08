# 04 — Object Pages, Properties & Editing

## 1. La fiche objet est le centre de gravité

Une fiche objet doit être lue comme l'exposition d'une **instance canonique** du repository.

Exemple :

```text
Class       : Application
Name        : MayaBank Payment Orchestrator
External ID : APP-PAY-0042
Owner       : Payments Domain
Lifecycle   : Strategic
Criticality : Critical
```

L'écran exact dépend de la solution/configuration ; le modèle mental ne change pas.

## 2. Six catégories de propriétés

### Identité

- nom ;
- identifiant ;
- alias ;
- description.

### Classification

- domaine ;
- type ;
- catégorie ;
- criticité.

### Responsabilité

- owner ;
- steward ;
- organisation responsable.

### Cycle de vie

- current status ;
- lifecycle category ;
- dates de transition/revue.

### Architecture

- standard ;
- target state ;
- strategic fit ;
- rationalization disposition selon solution.

### Traçabilité

- source ;
- external key ;
- last review ;
- commentaire de décision.

Les noms réels des attributs doivent être confirmés dans le métamodèle client.

## 3. Valeur ≠ texte libre par défaut

Si une propriété sert au reporting, préférer une valeur gouvernée.

Mauvais :

```text
Criticality = super critical
Criticality = High
Criticality = C1
```

Meilleur :

```text
Criticality ∈ controlled vocabulary
```

## 4. Mandatory vs important

Ne pas rendre obligatoire tout ce qui pourrait être utile.

Un attribut obligatoire doit généralement avoir :

- une justification métier ;
- une source ;
- un owner ;
- une règle de qualité ;
- une utilité de décision.

Sinon il génère des valeurs fictives juste pour passer la validation.

## 5. Modifier une propriété

Avant modification :

```text
Who owns this field?
What is the source?
Is it synchronized?
Will the change be overwritten?
What reports use it?
What decision does it affect?
```

## 6. Attribut synchronisé

Exemple : version technique issue d'une CMDB.

Mauvaise pratique : corriger manuellement dans HOPEX sans traiter la source.

Meilleure pratique :

```text
Detect mismatch
→ identify authoritative source
→ correct source or integration rule
→ resynchronize
→ verify HOPEX
```

## 7. Description utile

Une description ne doit pas répéter le nom.

Mauvais :

```text
Payment Orchestrator is a payment orchestrator.
```

Meilleur :

```text
Coordinates validation, fraud decision, routing and payment state for instant payment initiation. Does not own customer authentication or clearing settlement.
```

## 8. MayaBank — définition minimale d'une Application

Pour le masterbook :

```text
Identity
- Canonical Name
- External ID
- Description

Governance
- Owner
- Steward
- Source
- Last Review

Decision
- Lifecycle
- Criticality
- Domain

Architecture
- Supported capabilities/processes
- Integrations
- Technology dependencies
```

## 9. Validation avant sauvegarde logique

Même si l'interface autorise une valeur, l'utilisateur doit vérifier :

- classe correcte ;
- nom conforme ;
- owner existant ;
- source connue ;
- aucune contradiction avec lifecycle ;
- relations cohérentes.

## 10. Anti-patterns

- renseigner `N/A` partout ;
- utiliser Description comme base de données parallèle ;
- saisir plusieurs valeurs dans un champ texte ;
- modifier un champ synchronisé ;
- mettre l'owner dans le nom ;
- confondre lifecycle produit et status de saisie ;
- utiliser une propriété pour représenter une relation structurante.

## 11. Exercice

Créer sur papier la fiche `Payment Orchestrator` avec 15 propriétés maximum. Pour chaque propriété, indiquer :

```text
Type
Source
Owner
Allowed values
Quality rule
Decision/use case
```

Retirer toute propriété dont aucun usage n'est identifiable.