# 01 — Capability Architecture : rôle et méthode

Une business capability décrit ce que l'entreprise doit savoir faire de manière relativement stable, indépendamment de l'organisation, des processus ou des applications qui changent plus souvent.

```text
Strategy / Outcomes
        ↓
Business Capabilities
        ↓
Value Streams / Processes
        ↓
Applications / Data / Technology
        ↓
Projects / Investments
```

## Capability ≠ Process

- Capability : ce que l'entreprise sait ou doit savoir faire.
- Process : comment l'activité est exécutée.

Exemple MayaBank :

```text
Capability : Execute Instant Payments
Process    : Receive → Validate → Route → Settle → Notify
```

## Capability ≠ Organization

Une capability est une aptitude ; une Org-Unit est un acteur responsable ou contributeur.

## Capability ≠ Application

Une capability est un besoin métier durable ; une application est un moyen IT qui la supporte. Le mapping capability ↔ application permet d'identifier redondance, sous-couverture, dépendances critiques et opportunités de rationalisation.

## Méthode en 8 étapes

1. définir le scope ;
2. identifier les capabilities L0/L1 ;
3. décomposer uniquement quand nécessaire ;
4. valider les définitions ;
5. attribuer ownership et source ;
6. évaluer importance et maturité ;
7. mapper applications, data et technologies ;
8. dériver gaps, scénarios et roadmap.

## Règle de stabilité

Mauvais : `Use Kafka`, `Operate OpenShift`, `Run Oracle RAC`.

Meilleur : `Event Streaming`, `Container Platform Operations`, `Critical Data Persistence`.

## Questions que la carte doit permettre de traiter

- quelles capabilities sont stratégiques ?
- lesquelles sont faibles ?
- quelles applications les supportent ?
- où existe-t-il de la redondance ?
- quelles capabilities dépendent de technologies obsolètes ?
- quels programmes améliorent quelles capabilities ?
- où se concentrent les risques ?

Une capability map est utile lorsqu'elle permet une décision, pas seulement lorsqu'elle est visuellement propre.