# 08 — Governance, Quality Rules et Anti-patterns

## 1. Gouvernance minimale

Chaque capability doit avoir :

- identifiant canonique ;
- nom et définition ;
- niveau taxonomique ;
- parent ;
- owner/steward ;
- source ;
- date de revue ;
- statut ;
- méthode d'évaluation ;
- relations clés.

## 2. Change governance

Toute modification structurelle doit passer par :

```text
Proposal
→ Semantic review
→ Impact analysis
→ Owner approval
→ Repository update
→ View/report validation
→ Communication
```

## 3. Quality controls

Contrôles recommandés :

- capabilities sans owner ;
- définitions vides ;
- doublons suspects ;
- parents incohérents ;
- L3 sans parent L2 ;
- scoring périmé ;
- applications mappées à aucune capability ;
- capabilities stratégiques sans initiative ;
- initiatives sans gap associé ;
- target maturity inférieure au current sans justification.

## 4. Anti-patterns majeurs

### Capability = application
`Kafka`, `Salesforce`, `OpenShift` deviennent des pseudo-capabilities.

### Capability = équipe
`Payments Squad`, `Fraud Team` deviennent des capacités.

### Capability = process step
La carte descend jusqu'à des tâches opérationnelles.

### Everything is strategic
Toutes les capabilities reçoivent importance 5, donc le scoring ne discrimine plus rien.

### Heatmap theatre
On change les couleurs sans modifier les données ou la méthode d'évaluation.

### Framework cloning
Un modèle BIAN/APQC est importé et adopté sans adaptation ni ownership.

### Mapping inflation
Chaque capability est liée à toutes les applications du domaine pour éviter de choisir.

### Project-driven taxonomy
Chaque programme crée ses propres capabilities temporaires.

## 5. Review board questions

1. la capability est-elle durable ?
2. sa définition est-elle non ambiguë ?
3. le parent est-il correct ?
4. la granularité est-elle utile ?
5. le score est-il prouvé ?
6. le target est-il justifié ?
7. les mappings sont-ils sémantiques ?
8. le gap est-il relié à une initiative ?

## 6. Versioning

Conserver au minimum :

- date d'effet ;
- raison du changement ;
- approbateur ;
- impact sur mappings ;
- impact sur reports ;
- impact sur roadmaps.

## 7. KPI de qualité

```text
% capabilities with owner
% reviewed < 12 months
% strategic capabilities assessed
% strategic gaps linked to initiative
% orphan applications
% duplicate candidates
% taxonomy change rate
```

## 8. Règle finale

Une capability architecture est un produit de gouvernance d'entreprise, pas un atelier ponctuel. Sa valeur dépend de sa capacité à rester stable tout en intégrant les changements réellement nécessaires.