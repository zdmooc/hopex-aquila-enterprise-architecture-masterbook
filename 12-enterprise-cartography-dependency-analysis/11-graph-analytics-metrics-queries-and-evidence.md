# 11 — Graph Analytics, Metrics, Queries & Evidence

## 1. Pourquoi des métriques de graphe

Une cartographie visuelle devient difficile à exploiter à grande échelle. Des métriques simples permettent d’identifier les zones à investiguer.

Le principe :

```text
Metric
→ signal
→ investigation
→ architecture decision
```

Une métrique n’est jamais une décision automatique.

---

## 2. Important : frontière produit

Les métriques de graph theory de ce chapitre sont des **méthodes d’analyse génériques**.

Ce masterbook ne prétend pas que Hopex expose nativement chaque calcul ci-dessous.

Selon l’environnement, ils peuvent être réalisés :

- via fonctionnalités Hopex disponibles ;
- via GraphQL/REST/export ;
- dans un notebook/outillage externe ;
- avec un graph database temporaire ;
- avec des scripts de contrôle.

Le repository Hopex reste la source de contexte gouvernée.

---

## 3. Degree

Nombre total de relations d’un nœud.

Signal : objet très connecté.

Attention : mélange de relations hétérogènes peut rendre la métrique inutile.

---

## 4. In-degree

Nombre de relations entrantes selon une relation donnée.

Exemples :

```text
API consumers
Applications depending on platform
Processes supported by application
```

Un fort in-degree peut révéler un hub de dépendance.

---

## 5. Out-degree

Nombre de dépendances sortantes.

Exemple :

```text
Application
→ many external services
```

Peut signaler :

- coupling élevé ;
- surface de panne ;
- test complexity.

---

## 6. Reachability

Question : existe-t-il un chemin de A vers B ?

Exemple :

```text
Technology X
→ ...
→ Critical Business Service Y
```

Si oui, la technologie peut être dans la chaîne d’exposition du service.

---

## 7. Reachability set

Ensemble des objets atteignables depuis un point de départ selon règles de traversée.

Utilité : blast radius.

---

## 8. Reverse reachability

Ensemble des objets qui peuvent atteindre le nœud cible.

Utilité : trouver tous les consumers indirects.

---

## 9. Path length

Nombre d’arêtes entre deux objets.

Peut aider à distinguer :

```text
Direct consumer
Close indirect dependency
Distant contextual relationship
```

La gravité ne dépend pas seulement de la longueur.

---

## 10. Multiple paths

Deux objets peuvent être reliés par plusieurs chemins.

Exemple :

```text
Payment Orchestrator
→ Notification API
→ Notification

Payment Orchestrator
→ Event Streaming
→ Notification
```

Cela peut signifier :

- redondance ;
- transition ;
- multi-channel integration ;
- incohérence de modèle.

---

## 11. Path diversity

Plusieurs chemins indépendants peuvent améliorer la résilience, à condition qu’ils ne partagent pas un même failure domain.

```text
Path A and Path B
both depend on same DNS
```

=> diversité apparente seulement.

---

## 12. Centrality — concept

Les mesures de centralité cherchent les nœuds structurellement importants.

Exemples génériques :

- degree centrality ;
- betweenness centrality ;
- closeness centrality.

Usage : prioriser investigation.

Ne pas transformer un score de centralité en criticité métier.

---

## 13. Betweenness centrality — intuition

Un nœud situé sur beaucoup de chemins peut agir comme broker/bridge.

Exemple :

```text
Many domains
→ API Management
→ many services
```

Cela peut signaler un choke point architectural.

---

## 14. Closeness — usage prudent

Mesure la proximité moyenne d’un nœud dans le graphe.

Peut signaler un composant très central topologiquement, mais pas forcément important métier.

---

## 15. Connected components

Si le graphe se sépare en composantes indépendantes, cela peut révéler :

- domaines réels ;
- objets non intégrés ;
- trous de relation ;
- systèmes isolés.

---

## 16. Orphan ratio

Exemple pédagogique :

```text
orphan applications / total applications
```

Un taux élevé peut signaler un problème de qualité du repository.

---

## 17. Relation completeness

Pour les applications critiques :

```text
% with owner
% with process/capability
% with platform
% with data dependency
% with interface mapping
```

La complétude conditionne la fiabilité des analyses.

---

## 18. Dependency confidence metric

Exemple pédagogique :

```text
Verified = 1.0
Observed = 0.9
Imported current = 0.8
Inferred = 0.5
Stale = 0.2
```

Ces valeurs sont pédagogiques.

Objectif : identifier les zones nécessitant validation.

---

## 19. Freshness metric

```text
Age since last validation
```

Par exemple :

```text
0–90 days
91–180 days
>180 days
```

Seuils à définir selon la gouvernance réelle.

---

## 20. Relationship churn

Nombre de relations créées/modifiées/supprimées sur une période.

Peut signaler :

- transformation active ;
- instabilité de modèle ;
- import change ;
- besoin de revue.

---

## 21. Hub risk score — pédagogique

```text
Consumers count
× average criticality
× lack of fallback
× shared failure-domain factor
```

À utiliser pour prioriser une revue, pas comme vérité absolue.

---

## 22. Dependency debt

Définition pédagogique : dépendance problématique maintenue faute de remédiation.

Exemples :

- deprecated API ;
- shared DB ;
- unsupported technology ;
- temporary adapter ;
- unowned interface ;
- untested DR dependency.

---

## 23. Dependency debt register

| Dependency | Debt type | Risk | Owner | Target action | Due |
|---|---|---|---|---|---|
| Legacy API v1 | deprecated contract | High | Payments | migrate consumers | target date |
| Shared DB | coupling | High | Core | split ownership | roadmap |
| Old JVM | obsolescence | Medium | Platform | upgrade | roadmap |

---

## 24. Query library

Questions standard :

```text
Q1. Which critical applications use Technology X?
Q2. Which processes depend on Application Y?
Q3. Which consumers still use API v1?
Q4. Which critical applications have no DR dependency mapping?
Q5. Which applications depend on external provider Z?
Q6. Which nodes have high in-degree in runtime dependencies?
Q7. Which relations are stale?
Q8. Which target applications still depend on retired technology?
Q9. Which current applications have no target replacement?
Q10. Which critical paths cross a single site?
```

---

## 25. Query reproducibility

Une analyse doit documenter :

```text
Query purpose
Scope
Object types
Relation types
Filters
Date
Result count
Owner
```

Pour pouvoir la rejouer.

---

## 26. Query vs report

Query :

```text
find raw matching objects/paths
```

Report :

```text
present interpreted indicators
```

La Partie XV approfondira reporting et dashboards.

---

## 27. Evidence-first analytics

Une métrique n’est utile que si les données sources sont :

- complètes ;
- fraîches ;
- sourcées ;
- comprises ;
- cohérentes.

---

## 28. False precision

Éviter :

```text
Risk score = 83.427
```

si le repository contient 30 % de relations non validées.

Préférer :

```text
High concentration risk
Confidence: Medium
Missing: external dependencies for 4 apps
```

---

## 29. Confidence-aware result

Exemple :

```text
Known consumers: 12
Suspected consumers: 5
Unknown ownership: 2
Last validated: 2026-08
```

C’est plus honnête qu’un résultat unique non nuancé.

---

## 30. Graph export boundary

Si une analyse avancée est faite hors Hopex :

1. exporter IDs canoniques ;
2. conserver types d’objets ;
3. conserver types de relations ;
4. conserver source/confidence ;
5. calculer ;
6. réimporter seulement les résultats réellement gouvernables si nécessaire ;
7. ne pas créer un second repository concurrent.

---

## 31. Graph database usage

Un graph database peut être utilisé temporairement pour :

- path queries ;
- centrality ;
- cycle detection ;
- connected components.

Mais le masterbook ne recommande pas de remplacer Hopex par ce graph store.

---

## 32. API usage

Les APIs Hopex pourront être approfondies en Partie XX.

Principe :

```text
Repository
→ API/export
→ analysis
→ validated insight
→ architecture decision
```

---

## 33. MayaBank analytics catalogue

### A. High-consumer services

```text
IAM
API Management
Event Streaming
Core Account
```

### B. Deprecated dependency

```text
Legacy Payment Gateway
Legacy API v1
```

### C. Missing dependency evidence

```text
Critical applications with no platform relation
```

### D. Cross-domain concentration

```text
shared platforms used by Payments + Fraud + Customer
```

---

## 34. MayaBank — example insight

Supposons :

```text
IAM has 18 critical consumers
Kafka has 12 consumers
Legacy Gateway has 3 consumers
```

Conclusion correcte :

> IAM mérite une revue prioritaire de résilience et de DR.

Conclusion incorrecte :

> IAM est forcément le composant le plus critique.

---

## 35. Analytics governance

Pour chaque métrique :

- definition ;
- calculation ;
- source ;
- owner ;
- refresh ;
- threshold ;
- action.

---

## 36. Anti-patterns

- centrality = business criticality ;
- score sans definition ;
- query non reproductible ;
- graph export devenu source de vérité parallèle ;
- métrique sur données stale ;
- ranking présenté sans confidence ;
- dashboard sans action.

---

## 37. Questions d’entretien

**À quoi sert l’in-degree ?**  
À repérer notamment un objet ayant beaucoup de consommateurs selon une relation précise.

**Betweenness élevé signifie-t-il automatiquement SPOF ?**  
Non. C’est un signal de position structurante à confronter à HA, fallback et impact métier.

**Pourquoi mesurer la complétude avant le blast radius ?**  
Parce qu’un graph incomplet sous-estime mécaniquement les impacts.

**Peut-on utiliser un graph database avec Hopex ?**  
Oui comme outil complémentaire d’analyse si nécessaire, tout en conservant Hopex comme repository gouverné et en maîtrisant les synchronisations.
