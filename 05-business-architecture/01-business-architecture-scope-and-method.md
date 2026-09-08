# 01 — Business Architecture : rôle, périmètre et méthode

## 1. Pourquoi la Business Architecture existe

La Business Architecture traduit la stratégie en une représentation exploitable de l'entreprise : ce qu'elle veut accomplir, les capacités qu'elle doit posséder, la valeur qu'elle délivre, son organisation, ses services, ses produits et ses processus.

Elle répond notamment à cinq questions :

1. **Pourquoi changer ?** — drivers, objectifs, outcomes et contraintes.
2. **Qu'est-ce que l'entreprise doit savoir faire ?** — capabilities.
3. **Comment la valeur est-elle créée et délivrée ?** — value streams et customer journeys.
4. **Qui porte quoi ?** — organisation, rôles, responsabilités et ownership.
5. **Comment cela se traduit-il dans l'exécution ?** — services, produits, processus, information et systèmes supports.

Une Business Architecture mature ne se limite donc ni à un organigramme ni à une carte de processus.

## 2. Positionnement HOPEX

HOPEX est adapté à cette approche parce qu'il relie les perspectives business, IT, data et risk dans un repository commun.

Mental model :

```text
Strategy / Drivers
       ↓
Capabilities
       ↓
Value Streams / Customer Journeys
       ↓
Business Services / Products
       ↓
Processes / Organization
       ↓
Information
       ↓
Applications / Technologies
       ↓
Transformation initiatives
```

Le rôle du repository est de permettre de traverser ces niveaux sans recréer les mêmes objets dans chaque vue.

## 3. Les objets métier ne sont pas des dessins

Dans un repository gouverné :

```text
Business Capability = objet canonique
Business Process    = objet canonique
Org-Unit            = objet canonique
Business Service    = objet canonique
Value Stream        = objet canonique
```

Puis les diagrammes, matrices, listes et dashboards exploitent ces objets.

Une Capability Map n'est donc pas la vérité : c'est **une représentation d'objets du repository**.

## 4. Architecture métier vs organisation

Une organisation répond à :

```text
Qui ?
```

Une capability répond à :

```text
Qu'est-ce que l'entreprise sait faire ?
```

Un processus répond à :

```text
Comment le travail est-il exécuté ?
```

Un value stream répond à :

```text
Comment la valeur progresse-t-elle vers un stakeholder ?
```

Confondre ces quatre niveaux détruit la stabilité du modèle.

## 5. Business Architecture vs Business Process Management

Business Architecture :

- structure stratégique et opératoire ;
- capabilities ;
- value streams ;
- organisation ;
- services et produits ;
- alignement avec information, applications et transformation.

BPM/BPA :

- séquence des activités ;
- événements ;
- responsabilités de processus ;
- scénarios ;
- contrôles ;
- mesure de performance ;
- optimisation détaillée.

La Partie VII traitera ce niveau détaillé.

## 6. Business Architecture vs IT Architecture

La Partie IV partait essentiellement du paysage IT.

La Partie V part du besoin métier.

```text
Business Architecture
Capability → Value → Service → Process
                     ↓
                  Application
                     ↓
                  Technology
```

Cette direction évite de construire une architecture uniquement à partir des systèmes déjà existants.

## 7. Méthode en neuf étapes

### Étape 1 — cadrer la décision

Exemple MayaBank :

> Réduire le délai de mise à disposition d'un nouveau service de paiement tout en améliorant la résilience et la conformité.

### Étape 2 — identifier stakeholders, drivers et outcomes

```text
Customer
Operations
Compliance
Payments Business
CIO
Risk
```

### Étape 3 — cartographier les capabilities

Ne pas commencer par les applications.

### Étape 4 — représenter les value streams

Comprendre comment la valeur est créée de bout en bout.

### Étape 5 — identifier services et produits

Ce qui est réellement délivré aux stakeholders.

### Étape 6 — relier les processus structurants

Seulement au niveau nécessaire pour la décision.

### Étape 7 — relier organisation et ownership

Qui porte la capability ? Qui possède le processus ? Qui porte le service ?

### Étape 8 — relier applications, data et technology

La Business Architecture devient exploitable par l'EA.

### Étape 9 — analyser gaps et initiatives

Passer du modèle descriptif au modèle de transformation.

## 8. Les niveaux de granularité

Une carte métier trop grossière ne permet aucun arbitrage.

Une carte trop détaillée devient un inventaire ingérable.

Règle pratique :

```text
L0  Enterprise
L1  Domaines majeurs
L2  Capabilities / value streams utiles à la décision
L3  Sous-capabilities / processus structurants
L4+ Détail BPA ou opérationnel lorsque nécessaire
```

Les niveaux exacts dépendent du cadre d'entreprise, mais le principe est de conserver une granularité cohérente.

## 9. La vue n'est pas le modèle

Un même objet peut apparaître dans :

- Capability Map ;
- Value Stream View ;
- Customer Journey ;
- Organization View ;
- Process Architecture ;
- Business/Application Matrix ;
- Transformation Roadmap.

Ne jamais dupliquer l'objet uniquement pour adapter une vue.

## 10. Exemple MayaBank

Décision : moderniser les paiements instantanés.

```text
Driver
Instant payment growth + regulatory pressure

Outcome
Faster, resilient and compliant payment execution

Capabilities
Payment Initiation
Payment Orchestration
Fraud Decisioning
Payment Clearing
Customer Notification
Operational Monitoring

Value Stream
Initiate → Validate → Decide → Execute → Confirm

Business Service
Instant Payment Service

Processes
Execute Instant Payment
Handle Payment Exception
Investigate Fraud Alert

Applications
Payment Orchestrator
Fraud Engine
Notification Service
```

Cette chaîne devient le backbone de la Business Architecture MayaBank.

## 11. Deliverables utiles

Une Business Architecture n'a pas besoin de cent diagrammes.

Les livrables les plus utiles sont généralement :

1. context & stakeholder map ;
2. capability map ;
3. value stream map ;
4. business service/product catalog ;
5. organization responsibility map ;
6. high-level process architecture ;
7. business-to-application mapping ;
8. gap heatmap ;
9. transformation roadmap ;
10. decision log.

## 12. Questions d'entretien

**Quelle différence entre capability et process ?**  
La capability décrit une aptitude relativement stable de l'entreprise ; le processus décrit la manière dont le travail est exécuté.

**Pourquoi relier capabilities et applications ?**  
Pour comprendre comment le SI soutient le métier, détecter sur/sous-investissement, risques et opportunités de rationalisation.

**Pourquoi le value stream est-il utile ?**  
Parce qu'il recentre l'architecture sur la création de valeur de bout en bout au lieu de refléter uniquement les silos organisationnels.