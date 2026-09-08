# 01 — Repository as System of Record

## 1. Repository ≠ dossier de diagrammes

HOPEX prend toute sa valeur lorsque le repository devient une **source structurée de connaissance d'architecture** et non un simple emplacement où stocker des représentations.

Dans un usage faible :

```text
Diagramme A → Application X
Diagramme B → Application X bis
Excel C → Application X ancien nom
CMDB → CI Application X
```

Chaque vue porte sa propre vérité.

Dans un usage gouverné :

```text
Application X = objet canonique
  ├─ owner
  ├─ lifecycle
  ├─ criticality
  ├─ business support
  ├─ technologies
  ├─ interfaces
  ├─ data
  ├─ risks
  └─ transformation roadmap
```

Les diagrammes, rapports et APIs réutilisent le même objet.

## 2. Qu'est-ce qu'une source de vérité ?

Une source de vérité n'est pas forcément la source de **tous** les attributs.

Exemple MayaBank :

| Donnée | Source maîtresse possible | HOPEX |
|---|---|---|
| Application logique | HOPEX | objet canonique |
| CI serveur | CMDB ServiceNow | référence/synchronisation sélective |
| Owner métier | annuaire / gouvernance | propriété gouvernée |
| Version runtime | CMDB / discovery | donnée synchronisée si utile |
| Lifecycle stratégique | HOPEX / architecture board | décision EA |
| coût | outil financier | donnée importée/agrégée |

Le repository peut donc devenir un **system of record architectural** tout en consommant des données externes.

## 3. Les quatre responsabilités d'un repository EAM

### Identité
Savoir si deux informations parlent du même objet.

### Sémantique
Savoir ce que représente l'objet : Application, Business Capability, Process, Technology, Org-Unit, etc.

### Relations
Savoir comment l'objet dépend, supporte, réalise, appartient ou se connecte aux autres objets.

### Gouvernance
Savoir qui maintient l'information, quand elle doit être revue et quelle source est autoritative.

## 4. Objet canonique

Un objet canonique est la représentation de référence d'un concept gouverné.

Exemple :

```text
Name        : MayaBank Payment Orchestrator
Class       : Application
Owner       : Payments Domain
Lifecycle   : Strategic
Criticality : Critical
Source      : EA governance
```

Puis :

```text
Payment Orchestrator
→ supports Instant Payment Process
→ uses Fraud Decision Service
→ exchanges Payment Events
→ depends on PostgreSQL Platform
→ deployed on OpenShift Platform
```

## 5. Source, owner et steward

Trois notions doivent être séparées.

- **Source** : d'où provient la donnée.
- **Owner** : qui porte la responsabilité métier/architecturale de l'objet.
- **Steward** : qui entretient la qualité des informations dans le repository.

Une synchronisation automatique ne supprime pas la gouvernance.

## 6. Temporalité

Un repository d'architecture contient souvent plusieurs notions de temps :

- état actuel ;
- état cible ;
- lifecycle d'un objet ;
- date de revue ;
- date de fin de support ;
- roadmap de transformation.

Ne pas écraser toutes ces notions dans un unique champ `Status`.

## 7. Granularité

La granularité doit être guidée par les décisions à prendre.

Trop grossier :

```text
Application = Payments
```

Impossible de distinguer orchestration, fraude, notification, clearing.

Trop fin :

```text
1 objet HOPEX par microservice, pod, container et endpoint technique
```

Le repository devient une CMDB bis.

Meilleur compromis pour MayaBank :

```text
Architecture logique stable
→ Applications / capabilities / services majeurs

Runtime opérationnel volatil
→ CMDB / observability / platform tooling
```

## 8. Gouvernance de création

Avant de créer un objet :

1. rechercher si l'objet existe déjà ;
2. confirmer la MetaClass ;
3. appliquer la règle de nommage ;
4. renseigner l'identifiant externe si le processus d'intégration le prévoit ;
5. attribuer owner/steward ;
6. renseigner la source ;
7. créer uniquement les relations nécessaires ;
8. éviter les objets techniques sans usage d'analyse.

## 9. Gouvernance de modification

Une modification peut être :

- éditoriale ;
- sémantique ;
- structurelle ;
- issue d'une synchronisation ;
- issue d'une décision d'architecture.

Les changements structurels et de métamodèle doivent être plus gouvernés que la simple correction d'un libellé.

## 10. Gouvernance de suppression

Supprimer directement un objet peut casser :

- diagrammes ;
- analyses ;
- relations ;
- rapports ;
- intégrations.

Préférer un processus :

```text
Duplicate detected
→ determine canonical object
→ redirect relationships
→ validate impacts
→ archive/retire duplicate
→ delete only when safe
```

## 11. Mesures de qualité

Un repository mature suit au moins :

- taux d'objets sans owner ;
- taux d'objets sans lifecycle ;
- doublons suspects ;
- objets non revus depuis N mois ;
- relations orphelines ou incohérentes ;
- objets hors convention de nommage ;
- données synchronisées en erreur ;
- objets sans source identifiée.

## 12. MayaBank — définition du périmètre

Le repository du masterbook suit cette frontière :

```text
Business
Capability / Process / Org-Unit

Application
Application / Service / Interface / Flow

Data
Concept / Data Domain / Information Object

Technology
Software Technology / Platform / Standard

Transformation
Project / Initiative / Lifecycle / Target State
```

La nomenclature précise sera alignée sur les solutions HOPEX abordées dans les parties suivantes.

## 13. Questions d'entretien

**Pourquoi ne pas charger toute la CMDB dans HOPEX ?**  
Parce que le niveau de volatilité et la granularité opérationnelle peuvent dépasser le besoin d'architecture. On synchronise seulement ce qui sert une analyse EA.

**Quelle est la première qualité d'un repository ?**  
La capacité à identifier des objets canoniques et à maintenir des responsabilités claires.

**Que vaut une architecture si les relations ne sont pas gouvernées ?**  
Elle devient rapidement impossible à analyser automatiquement.
