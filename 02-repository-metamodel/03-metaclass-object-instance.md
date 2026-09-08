# 03 — MetaClass, Object & Instance

## 1. MetaClass vs objet

La confusion la plus fréquente est de mélanger le **type** et l'**instance**.

```text
MetaClass = Application
Object    = MayaBank Payment Orchestrator
```

La MetaClass définit ce qu'est une application dans le repository. L'objet représente une application réelle de l'entreprise.

## 2. Instance

Une instance hérite de la structure autorisée par sa MetaClass :

- propriétés ;
- associations ;
- classifications ;
- règles de validation ;
- possibilités de navigation et d'analyse.

Mental model :

```text
MetaClass Application
       ↓ instanciation
Payment Orchestrator
Fraud Engine
Notification Service
Clearing Adapter
```

## 3. Pourquoi cela change la façon de modéliser

Dans PowerPoint, une boîte n'a pas besoin d'être typée rigoureusement.

Dans un repository :

```text
Payment Orchestrator
```

ne peut pas être à la fois :

- Application ;
- Business Capability ;
- Server ;
- Project ;

selon le diagramme du jour.

La classification sémantique doit être stable.

## 4. Nom visible ≠ identité

Le nom est une propriété utile aux utilisateurs, mais il ne doit pas être le seul mécanisme d'identification.

Deux objets peuvent partager un nom dans des contextes différents ; inversement un même objet peut être renommé sans devenir un nouvel objet.

Règle :

```text
identity != display name
```

## 5. Cycle de vie d'une instance

Une instance traverse souvent :

```text
Create
→ Enrich
→ Validate
→ Publish/use
→ Review
→ Retire/archive
```

La suppression physique immédiate n'est généralement pas la première réponse à l'obsolescence.

## 6. Objets logiques et objets techniques

MayaBank doit séparer les objets stables des instances techniques volatiles.

### Stable

```text
Payment Orchestrator
Instant Payment Capability
Fraud Management Process
OpenShift Platform Standard
```

### Volatil

```text
pod payment-orchestrator-7f6f9c
VM vm1234
container sha256:...
```

HOPEX doit recevoir la granularité qui soutient l'analyse d'architecture, pas automatiquement chaque instance runtime.

## 7. Objet métier vs objet outil

Ne pas créer un objet pour refléter un artefact documentaire.

Mauvais :

```text
Application Payment Diagram V2
```

comme application.

Le diagramme est une représentation. L'objet architecture est la réalité modélisée.

## 8. Règle de création d'instance

Avant création :

1. quelle MetaClass ?
2. quelle définition exacte ?
3. existe-t-elle déjà ?
4. quelle source maîtresse ?
5. quel owner ?
6. quelle clé externe si import ?
7. quelles propriétés minimales ?
8. quelles relations sont nécessaires ?
9. quelle politique de revue ?

## 9. Exemple MayaBank — applications

Objets proposés :

| Objet | Type logique | Rôle |
|---|---|---|
| Payment Orchestrator | Application | orchestration paiement |
| Fraud Engine | Application | décision fraude |
| Clearing Adapter | Application | connexion rail externe |
| Notification Service | Application | notification client |

Ces objets peuvent ensuite être reliés à :

- capabilities ;
- business processes ;
- data ;
- technologies ;
- organizations ;
- roadmaps.

## 10. Exemple MayaBank — mauvaise granularité

Mauvais :

```text
Payment Orchestrator Prod
Payment Orchestrator Preprod
Payment Orchestrator Dev
Payment Orchestrator Site A
Payment Orchestrator Site B
```

si ces lignes représentent en réalité la même application logique.

On préférera un objet logique puis, si nécessaire, des relations vers des environnements ou déploiements.

## 11. Objets canoniques et vues

```text
Object Payment Orchestrator
  ↓ reused by
Application Map
Capability Map
Technology Impact View
Roadmap
Risk View
API query
```

C'est la réutilisation de la même instance qui évite la divergence.

## 12. Entretien

**Différence MetaClass / instance ?**  
La MetaClass définit le type et la structure ; l'instance représente un élément réel du repository.

**Pourquoi ne pas créer un objet par environnement ?**  
Parce qu'on risque de confondre architecture logique et déploiement. On ne sépare que si le métamodèle et le besoin d'analyse le justifient.
