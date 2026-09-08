# 04 — Portfolio de solutions et cas d'usage

## 1. Pourquoi parler de solutions

HOPEX n'est pas une fonctionnalité unique. Le repository est exploité par plusieurs solutions répondant à des préoccupations différentes.

Pour l'architecte, il faut donc toujours demander :

```text
Quel problème métier / architecture ?
→ quelle solution HOPEX ?
→ quels objets ?
→ quelles propriétés ?
→ quelles relations ?
→ quels rapports / décisions ?
```

## 2. HOPEX IT Architecture

Objectif général : représenter et analyser l'architecture IT.

Exemples de préoccupations :

- applications ;
- services applicatifs ;
- technologies ;
- dépendances ;
- standards ;
- obsolescence ;
- alignement avec le métier ;
- transformations.

Cas MayaBank : comprendre les dépendances de la plateforme Instant Payment entre API, orchestrateur, fraude, clearing, event streaming, bases et plateformes.

## 3. IT Business Management

ITBM aide à rapprocher les actifs IT des enjeux de pilotage métier.

Questions typiques :

- quelle valeur métier fournit une application ?
- quel owner ?
- quelle criticité ?
- quels coûts ou risques ?
- quelle stratégie de maintien, modernisation ou retrait ?

Cas MayaBank : comparer plusieurs applications de paiement historiques avec la cible temps réel.

## 4. IT Portfolio Management

ITPM vise le pilotage et la rationalisation du portefeuille IT.

Exemples :

- portefeuille applicatif ;
- lifecycle ;
- redondances ;
- technologies obsolètes ;
- décisions invest / tolerate / migrate / retire selon les méthodes retenues ;
- trajectoires de transformation.

La terminologie exacte des dashboards et évaluations dépend de la solution/version/configuration.

## 5. Business Process Analysis

BPA permet de travailler sur les processus métier et leurs relations avec les acteurs, informations, applications et risques.

Cas MayaBank :

```text
Initiate Payment
→ Validate
→ Fraud Decision
→ Execute
→ Settle
→ Notify
→ Reconcile
```

Le but n'est pas seulement de dessiner le workflow mais de relier le processus au référentiel d'entreprise.

## 6. Information Architecture

Cette perspective aide à structurer :

- concepts d'information ;
- objets métier / informationnels ;
- responsabilités ;
- usages ;
- relations avec processus et applications.

Cas MayaBank : Payment Order, Payment Transaction, Account, Fraud Decision, Settlement Status.

## 7. Data Governance

Data Governance se concentre davantage sur la gouvernance des données : ownership, qualité, classification, politiques et responsabilités selon le périmètre de la solution.

Cas MayaBank : déterminer qui possède la définition du Payment Status, quelles applications le produisent et où se trouvent les sources de vérité.

## 8. Integrated Risk Management

IRM couvre des préoccupations de risque et de contrôle. Pour l'architecture d'entreprise, l'intérêt est la capacité à relier :

```text
Business / Application / Technology
↔ Risk
↔ Control
↔ Compliance
```

Cas MayaBank : associer risques de disponibilité, cyber et conformité aux objets concernés.

## 9. Une même entreprise, plusieurs perspectives

Exemple : `Payment Orchestrator`.

Dans IT Architecture :
- dépendances applicatives/technologiques.

Dans ITBM/ITPM :
- owner, lifecycle, criticité, portefeuille.

Dans BPA :
- support de processus de paiement.

Dans Data/Information :
- données utilisées/produites.

Dans IRM :
- risques et contrôles.

Le gain vient du **même objet connecté**, pas de six copies.

## 10. Architecture concern map

| Stakeholder | Concern | Perspective HOPEX |
|---|---|---|
| CIO | portefeuille et transformation | ITBM / ITPM / EA |
| Enterprise Architect | cohérence cross-domain | EA / IT Architecture |
| Solution Architect | dépendances solution | IT Architecture |
| Business Architect | capabilities/processes | Business Architecture/BPA |
| Data Architect | information/data | Information Architecture/Data Governance |
| CISO/Risk | risques/contrôles | IRM + architecture |
| Operations | réalité run | intégration ServiceNow + architecture |

## 11. Anti-pattern : acheter la solution avant le use case

Mauvaise démarche :

```text
Nous avons HOPEX → remplissons tous les champs.
```

Bonne démarche :

```text
Décision à prendre
→ données nécessaires
→ modèle minimum
→ source
→ gouvernance
→ rapport / analyse
→ enrichissement progressif
```

## 12. Cas d'entretien

**Comment éviter un repository trop complexe ?**
En partant des décisions attendues et en limitant le métamodèle opérationnel aux objets/propriétés réellement gouvernés.

**Pourquoi relier architecture et portfolio ?**
Parce qu'une dépendance technique sans lifecycle ni décision de transformation ne suffit pas pour piloter un SI.

**Pourquoi relier BPA et applications ?**
Pour mesurer l'impact d'une évolution applicative sur les activités métier et inversement.
