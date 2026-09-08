# 01 — Relationships, Diagrams, Matrices & Views : rôle, périmètre et méthode

## 1. Objectif

Cette partie explique comment transformer un repository HOPEX en **système de connaissance navigable et lisible**.

Les objets seuls ne suffisent pas. La valeur apparaît lorsque l’on maîtrise :

```text
Objects
+ semantic relationships
+ scoped views
+ matrices
+ filters
+ visual conventions
+ governance
= decision-ready architecture
```

Le but n’est donc pas de produire « plus de dessins », mais de produire des représentations fiables qui répondent à des décisions concrètes.

## 2. Frontières avec les autres parties

```text
Partie II — Repository & Metamodel
→ MetaAssociation, MetaAssociationEnd, cardinalité, objet canonique

Partie III — UI & Navigation
→ ouverture, navigation, utilisation de listes, matrices et diagrammes

Partie XI — Relationships, Diagrams, Matrices & Views
→ sémantique, patterns de représentation, qualité, gouvernance, standards visuels

Partie XII — Enterprise Cartography & Dependency Analysis
→ analyse de graphe et cartographie entreprise à grande échelle

Partie XV — Reports & Dashboards
→ reporting, indicateurs et decision support
```

## 3. Relation > trait graphique

Une relation doit exister pour une raison architecturale.

Exemple :

```text
Payment Orchestrator
→ supports
Execute Instant Payment
```

Ce lien doit pouvoir alimenter :

- navigation ;
- matrice ;
- impact analysis ;
- vue cross-layer ;
- requête API ;
- reporting.

Un trait dessiné uniquement pour améliorer une image n’a pas cette valeur.

## 4. Diagramme = représentation

Le diagramme est une projection du repository.

```text
Canonical object
→ represented in View A
→ represented in View B
→ represented in Matrix C
```

Le déplacement graphique d’un objet ne doit pas créer un nouvel objet sémantique.

## 5. Matrice = couverture

Une matrice est adaptée aux relations many-to-many.

Exemples :

```text
Capability × Application
Process × Application
Application × Technology
Application × Information
Risk × Control
Initiative × Capability
```

Elle est préférable au diagramme quand la question principale est :

> qui couvre quoi ?

## 6. View = concern + scope + rules

Une vue de qualité précise :

```text
Stakeholder
Concern
Scope
Time horizon
Included object types
Included relation types
Visual rules
Decision expected
```

Sans cela, la vue devient une image générique.

## 7. Les cinq représentations principales

### Diagram
Pour structure, flux, interactions, dépendances.

### Matrix
Pour couverture et comparaison many-to-many.

### List
Pour propriétés, triage, revue, complétude.

### Heatmap / overlay
Pour faire ressortir une dimension de décision.

### Dashboard / report
Pour agrégation et indicateurs — approfondis en Partie XV.

## 8. Méthode en dix étapes

1. Définir la question.
2. Identifier le stakeholder.
3. Identifier les objets canoniques nécessaires.
4. Choisir les relations utiles.
5. Choisir le bon type de représentation.
6. Définir scope et temporalité.
7. Appliquer des conventions visuelles.
8. Vérifier lisibilité et qualité des relations.
9. Publier avec owner et cycle de revue.
10. Supprimer les vues qui n’ont plus d’usage.

## 9. Granularité

### Executive

```text
Strategy
→ Capabilities
→ Major applications
→ Transformation initiatives
```

### Enterprise Architecture

```text
Capabilities
→ Processes
→ Applications
→ Information
→ Platforms
```

### Solution Architecture

```text
Application services
→ interfaces
→ dependencies
→ deployments
→ NFR context
```

### Technical detail

À utiliser seulement si nécessaire à une décision.

## 10. MayaBank — exemple de concern

Question :

> Quel est l’impact du retrait de Legacy Payment Gateway ?

Vue minimale :

```text
Legacy Payment Gateway
→ consuming applications
→ supported process
→ capabilities
→ technologies
→ replacement application
→ migration initiative
```

Matrice complémentaire :

```text
Consumer Application × Interface
```

## 11. Faits produit vérifiés

Les pages publiques Bizzdesign Hopex consultées en septembre 2026 mettent en avant :

- repository unifié et connecté ;
- visualisations et diagrammes ;
- rapports, dashboards et portail d’entreprise ;
- vues self-service par stakeholder ;
- impact analysis ;
- partage des modèles via Hopex 360 dans des cas clients publics.

Le détail exact des types de diagrammes, matrices et écrans dépend des solutions, profils et configurations activés.

## 12. Règles de qualité

Une représentation doit :

- répondre à une question ;
- reposer sur des objets canoniques ;
- utiliser des relations définies ;
- afficher un scope explicite ;
- montrer current/target sans ambiguïté ;
- être compréhensible sans explication orale obligatoire ;
- éviter la surcharge graphique ;
- pouvoir être maintenue.

## 13. Anti-patterns

- mega-diagram de 300 objets ;
- relation générique « linked to » pour tout ;
- couleurs sans légende ;
- current et target mélangés ;
- copie manuelle d’un objet pour un second diagramme ;
- matrice trop grande non filtrée ;
- flèches sans direction sémantique ;
- vue sans owner ;
- diagramme utilisé comme base de données.

## 14. Questions d’entretien

**Pourquoi les relations sont-elles plus importantes que les diagrammes ?**  
Parce qu’elles structurent le graphe réutilisable par les vues, matrices, analyses, APIs et rapports.

**Quand préférer une matrice ?**  
Quand la question porte sur la couverture, la responsabilité ou une comparaison many-to-many.

**Qu’est-ce qu’une bonne vue ?**  
Une projection ciblée du repository, construite pour un stakeholder, un concern, un scope et une décision.