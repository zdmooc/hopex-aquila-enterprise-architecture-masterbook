# 03 — Relationship Governance, Evidence, Confidence & Data Quality

## 1. Une relation peut être fausse

Le repository n’est pas fiable uniquement parce qu’une relation existe.

Chaque relation critique doit pouvoir être évaluée selon :

```text
source
owner
confidence
last review date
validity period
acquisition method
```

## 2. Sources possibles

### Manual architect assertion

Relation saisie et validée par un architecte ou owner.

### Authoritative system

Exemple : relation de déploiement issue d’une CMDB ou d’un outil de discovery.

### Import

Excel, API, repository externe, catalogue technique.

### Inference

Relation calculée ou déduite.

Une inference doit être signalée comme telle.

## 3. Source of truth par type de relation

Exemple MayaBank :

| Relation | Source privilégiée |
|---|---|
| Application → Capability | Architecture/Business owners |
| Application → Technology | Architecture + discovery/CMDB |
| Application → Deployment | CMDB/platform tooling |
| Process → Application | Process owner + architect |
| Data → Owner | Data Governance |
| Technology lifecycle | Vendor/IT-Pedia + governance interne |

Le bon système de référence dépend du contexte client.

## 4. Confidence score

Taxonomie pédagogique :

```text
Verified
High confidence
Medium confidence
Low confidence
Inferred
Unknown
```

Le score ne doit pas remplacer une source ; il qualifie la confiance dans l’information.

## 5. Evidence date

Une relation peut être correcte aujourd’hui et fausse dans six mois.

Exemple :

```text
Payment Orchestrator
→ deployed on
OCP-PROD-EU
Evidence date: 2026-09-01
```

## 6. Validity interval

Pour une transition :

```text
Legacy Gateway → used by → Channel
valid until cutover
```

et :

```text
Payment Orchestrator → used by → Channel
valid from migration wave
```

Le mécanisme concret dépend du métamodèle et des capacités client.

## 7. Ownership

Une relation critique doit avoir un owner implicite ou explicite par règle de gouvernance.

Exemple :

```text
Application-to-Technology relationships
Accountable role = Technology Architecture
```

Il n’est pas toujours nécessaire de stocker un owner sur chaque relation si la gouvernance définit clairement le propriétaire du type de donnée.

## 8. Review frequency

Exemple de politique :

```text
Critical application dependencies → quarterly
Business capability support → twice yearly
Technology lifecycle → monthly/quarterly feed
Transformation links → each architecture gate
```

Les fréquences réelles doivent suivre le contexte client.

## 9. Stale relationships

Détecter :

- relation jamais revue ;
- source disparue ;
- endpoint retiré ;
- application retired mais toujours consommatrice ;
- technology replaced mais relation toujours active ;
- relation importée non rafraîchie.

## 10. Contradiction

Exemple :

```text
Manual relation: App runs on VM
CMDB feed: App runs on OpenShift
```

Ne pas choisir automatiquement l’une ou l’autre sans règle.

Processus :

```text
detect
→ classify
→ assign owner
→ resolve
→ document exception
```

## 11. Duplicate relationships

Deux liens identiques peuvent provenir de deux imports différents.

La déduplication doit considérer :

- endpoints ;
- relation type ;
- environment/scope ;
- source ;
- temporal validity.

## 12. Orphan relationship

Une relation vers un objet obsolète ou placeholder indique souvent :

- mauvais merge ;
- import partiel ;
- suppression non propagée ;
- erreur d’identité canonique.

## 13. Relationship completeness

Exemple : chaque application critique doit avoir au moins :

```text
Business owner / IT owner
Supported capabilities/processes
Key technologies/platforms
Critical upstream/downstream dependencies
Key data
Lifecycle/target direction
```

La complétude doit être définie par cas d’usage, pas par perfection théorique.

## 14. Referential integrity

Les liens doivent viser des objets canoniques existants et approuvés.

Mauvais :

```text
Payment Orchestrator → uses → "Kafka prod"
```

si `Kafka prod` est du texte libre alors qu’une plateforme canonique existe.

## 15. Acquisition method

Tag possible :

```text
manual
imported
discovered
calculated
inferred
```

Cela aide à décider comment corriger une donnée.

## 16. Automated feed vs manual edit

Une relation gérée par un feed automatique ne doit pas être corrigée manuellement sans stratégie, sinon la correction sera écrasée.

Préférer :

```text
fix source
or
apply governed override
```

## 17. Relationship quality KPIs

Exemples :

```text
% critical apps with verified dependencies
% relations with evidence date
% relations older than review threshold
% orphan relationships
% duplicate relationships
% inferred relations awaiting validation
```

Les dashboards seront approfondis en Partie XV.

## 18. MayaBank — quality gate

Pour `Payment Orchestrator`, la vue ne doit être publiée comme « production dependency map » que si :

- providers/consumers validés ;
- platform relation sourcée ;
- critical data links validés ;
- relation vers clearing confirmée ;
- ownership connu ;
- date de revue visible.

## 19. Relationship backlog

Catégories :

```text
Missing
Suspect
Stale
Duplicate
Conflicting
Unowned
Inferred-not-validated
```

## 20. Workflow de correction

```text
Detect issue
→ Assign steward/architect
→ Validate source
→ Correct canonical objects
→ Correct relation
→ Re-run impacted views/matrices
→ Close with evidence
```

## 21. Anti-patterns

- croire qu’un import est automatiquement vrai ;
- relation sans date ni source ;
- correction manuelle d’un feed automatique ;
- relations « inferred » présentées comme factuelles ;
- aucune stratégie de stale data ;
- vouloir 100 % de relations sur tout le SI avant d’obtenir de la valeur.

## 22. Questions d’entretien

**Comment fiabiliser une dependency map ?**  
En gouvernant la source, la date, le niveau de confiance et le processus de validation des relations critiques.

**Que faire si deux sources se contredisent ?**  
Appliquer une règle d’autorité par type de donnée et traiter l’écart comme une anomalie à résoudre.

**Pourquoi distinguer discovered et verified ?**  
Parce qu’une relation détectée techniquement n’est pas nécessairement l’interprétation architecturale correcte.