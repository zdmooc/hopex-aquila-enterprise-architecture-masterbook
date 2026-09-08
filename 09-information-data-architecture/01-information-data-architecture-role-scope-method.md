# 01 — Information & Data Architecture : rôle, périmètre et méthode

## 1. Pourquoi une architecture de l’information

L’Information & Data Architecture décrit **ce que signifient les données, où elles sont maîtrisées, comment elles circulent, comment elles sont transformées et comment elles soutiennent le métier et le SI**.

Elle doit permettre de répondre à des questions concrètes :

- quelles informations sont critiques pour une capability ou un processus ?
- quelle application est système de référence pour une information donnée ?
- où une donnée est-elle créée, transformée, copiée et consommée ?
- quels modèles décrivent sa structure ?
- qui en est owner et steward ?
- quelles règles de qualité s’appliquent ?
- quelles données sont sensibles ?
- quelles dépendances seraient impactées par un changement ?
- quelles duplications sont légitimes et lesquelles sont dangereuses ?
- quels objets doivent être conservés dans HOPEX et lesquels appartiennent à un data catalog technique ou à une CMDB ?

## 2. Information ≠ Data

Dans ce masterbook :

```text
Information
= sens métier porté par les données

Data
= représentation structurée ou non structurée de cette information
```

Exemple MayaBank :

```text
Information concept
Customer Identity

Logical data entities
Customer
Identity Document
Address

Physical representations
CUSTOMER table
JSON customer profile
Kafka event payload
```

La même information métier peut donc exister sous plusieurs représentations physiques.

## 3. Objectifs d’un architecte data

L’architecte doit articuler quatre couches :

```text
Business meaning
↓
Conceptual model
↓
Logical model
↓
Physical / implementation model
```

et les relier aux couches d’architecture :

```text
Capability
→ Process
→ Application
→ Information/Data
→ Technology
```

## 4. Ce que HOPEX apporte

HOPEX Aquila relie dans un repository commun les perspectives métier, IT, data et risques. Les capacités publiques de HOPEX Data Governance incluent notamment business glossary, data catalog, functional data lineage, data modeling, analyses et collaboration.

Dans cette partie, on utilise HOPEX comme **repository d’architecture et de gouvernance**, pas comme substitut universel à toutes les plateformes de données opérationnelles.

## 5. Frontières avec les autres parties

```text
Partie VIII
Application Architecture
→ applications, interfaces, responsabilités applicatives

Partie IX
Information & Data Architecture
→ sens, modèles, ownership, lineage, quality, lifecycle des données

Partie X
Technology & Infrastructure Architecture
→ moteurs DB, stockage, compute, cloud, OpenShift, infra

Partie XVI
Repository Governance & Data Quality
→ qualité du repository HOPEX lui-même
```

## 6. Les 10 artefacts fondamentaux

Une mission Information & Data Architecture devrait au minimum produire :

1. Information Concept Map.
2. Data Domain Map.
3. Business Glossary.
4. Conceptual Data Model.
5. Logical Data Model.
6. System-of-Record / Source-of-Truth Matrix.
7. Data Flow / Functional Lineage.
8. Data Quality Rule Catalogue.
9. Data Classification & Privacy Map.
10. Current / Target Data Architecture.

## 7. Méthode en 12 étapes

### Étape 1 — définir le scope métier

Exemple : `Execute Instant Payment`.

### Étape 2 — identifier les informations critiques

```text
Payment Instruction
Customer Identity
Account
Fraud Decision
Clearing Result
Payment Status
```

### Étape 3 — définir les data domains

Exemple : Customer, Account, Payment, Fraud, Reference Data, Risk.

### Étape 4 — nommer les owners

Un domaine sans ownership devient rapidement un catalogue documentaire sans gouvernance.

### Étape 5 — construire le modèle conceptuel

Identifier concepts et relations métier sans détails techniques.

### Étape 6 — construire ou relier le logical model

Entités, attributs structurants, relations, cardinalités, clés métier.

### Étape 7 — identifier systems of record

Pour chaque information critique :

```text
authoritative source
+ consuming systems
+ replicas/caches
+ derived datasets
```

### Étape 8 — tracer les flux

Inclure origine, destination, transformation, fréquence, protocole ou mode d’échange si utile.

### Étape 9 — analyser qualité et contrôles

Complétude, validité, unicité, cohérence, fraîcheur, exactitude selon le besoin.

### Étape 10 — classifier les données

Public / Internal / Confidential / Restricted, ou taxonomie client.

### Étape 11 — analyser current vs target

Identifier duplication, shared database, silos, absence d’owner, mappings manuels, batch tardifs, incohérences.

### Étape 12 — définir la roadmap

Prioriser par risque, valeur métier et dépendances.

## 8. Granularité

Un masterbook d’architecture n’a pas besoin de toutes les colonnes de toutes les bases.

Le niveau pertinent dépend de la décision :

```text
Strategy
→ Data Domain

Enterprise Architecture
→ Information Concept / Business Data

Solution Architecture
→ Logical Entity / Data Flow

Detailed Design
→ Table / Column / Schema
```

## 9. Règle anti-inventaire

Un bon modèle ne cherche pas à reproduire intégralement :

- le schéma de production ;
- le catalogue Kafka ;
- le DDL ;
- les objets de stockage ;
- les vues matérialisées ;
- les topics temporaires.

Il sélectionne les éléments qui permettent analyse, gouvernance et transformation.

## 10. MayaBank — baseline

Le fil rouge Part IX s’appuie sur :

```text
Customer
Account
Payment
Fraud
Clearing
Notification
Reference Data
Operations
```

avec le processus critique :

```text
Execute Instant Payment
```

## 11. Questions d’entretien

**Pourquoi distinguer information et donnée ?**  
Parce que le sens métier doit survivre aux changements de représentation technique.

**Pourquoi un conceptual data model ?**  
Pour aligner métier, data et architecture sur les concepts indépendamment des solutions techniques.

**Pourquoi le lineage est-il important ?**  
Pour comprendre provenance, transformations, dépendances et impacts d’un changement.

**HOPEX remplace-t-il un data lake catalog technique ?**  
Non par principe. HOPEX apporte gouvernance, architecture, contexte et relations ; les outils spécialisés peuvent enrichir le repository selon l’écosystème.
