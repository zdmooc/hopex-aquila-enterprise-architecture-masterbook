# 11 — IT Architecture Governance & Anti-patterns

## 1. Architecture gouvernée ≠ architecture dessinée

Le repository devient utile lorsque les données d'architecture sont maintenues selon des responsabilités et des règles explicites.

```text
Object
→ Owner
→ Source
→ Lifecycle
→ Review Date
→ Relationships
→ Decision / Action
```

Un diagramme sans cette gouvernance vieillit vite.

## 2. RACI minimal

| Objet | Accountable | Responsible |
|---|---|---|
| Application | Domain/Application Owner | Application Architect |
| Technology | Technology Owner | Technology Architect |
| Interface | Provider Owner | API/Integration Architect |
| Platform | Platform Owner | Platform Architect |
| Lifecycle | Architecture Governance | Object Owner |
| Roadmap | Transformation Owner | Lead Architect |

Les rôles réels doivent être adaptés à l'organisation.

## 3. Quality gates

Avant publication d'une architecture :

### Gate 1 — identité

- objets déjà recherchés ?
- doublons écartés ?
- nommage conforme ?

### Gate 2 — sémantique

- bonne MetaClass ?
- relations significatives ?
- granularité correcte ?

### Gate 3 — gouvernance

- owner ?
- source ?
- lifecycle ?
- date de revue ?

### Gate 4 — architecture

- current compris ?
- target cohérente ?
- standards respectés ?
- impacts analysés ?

### Gate 5 — transformation

- initiatives reliées ?
- milestones ?
- coexistence ?
- decommissioning ?

## 4. Architecture review checklist

### Business alignment

- capability/process support identifiable ;
- criticité business comprise ;
- exigences structurantes tracées.

### Application

- applications canoniques ;
- responsabilités non ambiguës ;
- interfaces/flows critiques ;
- duplication évaluée.

### Technology

- technologies utilisées ;
- lifecycle/support ;
- standard status ;
- exceptions documentées.

### Deployment

- plateformes ;
- shared services ;
- HA/DR ;
- trust boundaries ;
- SPOF.

### Transformation

- current/target ;
- transitions ;
- dependencies ;
- exit legacy.

## 5. Anti-pattern — repository comme PowerPoint

Symptômes :

- beaucoup de diagrammes ;
- peu de propriétés ;
- relations génériques ;
- duplication d'objets ;
- analyses impossibles.

Correction : revenir aux objets canoniques et aux questions de décision.

## 6. Anti-pattern — CMDB bis

Symptômes :

```text
10 000 VMs
40 000 pods
200 000 endpoints
```

mais aucune capability, target ou roadmap.

Correction : garder les dépendances d'architecture stables et référencer la CMDB pour le runtime.

## 7. Anti-pattern — catalogue mort

Un inventaire applicatif non maintenu devient rapidement faux.

Mesures :

- `% applications sans owner` ;
- `% lifecycle non revu` ;
- `% applications sans capability/process` ;
- `% technologies sans source` ;
- `% relations non revues`.

## 8. Anti-pattern — target wish list

```text
Cloud
Microservices
Kafka
AI
Zero Trust
```

ne constitue pas une architecture cible.

Il faut :

- responsabilités ;
- dépendances ;
- standards ;
- exigences ;
- migration ;
- risques ;
- trade-offs.

## 9. Anti-pattern — relation universelle

```text
Connected To
Connected To
Connected To
```

empêche l'analyse sémantique.

Préférer les relations proposées par le métamodèle et les compléter avec des propriétés seulement lorsque nécessaire.

## 10. Anti-pattern — produit = architecture

Exemple :

```text
OpenShift
Kafka
Oracle
```

Une liste de produits ne dit pas :

- quels services ils fournissent ;
- qui les utilise ;
- pourquoi ;
- comment ils participent à la cible.

## 11. Anti-pattern — statut manuel dans les vues

Une couleur rouge peinte sur une boîte est fragile.

Meilleur :

```text
Lifecycle property
→ rule
→ heatmap/report
```

La visualisation doit être dérivée des données lorsque possible.

## 12. Anti-pattern — suppression du legacy trop tôt

Un objet `Retired` alors que des flux l'utilisent encore fausse le repository.

Processus :

```text
Retire decision
→ migration
→ consumers removed
→ flows closed
→ runtime decommissioned
→ final lifecycle update
```

## 13. Anti-pattern — découverte automatique = vérité

Discovery apporte des facts techniques, mais peut :

- créer des doublons ;
- exposer une granularité trop fine ;
- mal classifier ;
- manquer le contexte métier.

Toute ingestion doit avoir une règle de reconciliation.

## 14. Anti-pattern — custom metamodel immédiat

Avant création d'un objet custom :

```text
standard MetaClass ?
property ?
classifier ?
existing association ?
```

Le custom est traité en profondeur en Partie XVIII.

## 15. Architecture board

Questions à demander en revue :

1. quel concern est traité ?
2. quelle est la source des facts ?
3. quel current ?
4. quelles options ont été étudiées ?
5. quel target ?
6. quels trade-offs ?
7. quels risques ?
8. quelles dépendances ?
9. quelle roadmap ?
10. quel legacy sort réellement ?

## 16. Evidence pack

Un dossier de revue peut référencer :

- vues HOPEX ;
- listes d'objets ;
- technology compliance ;
- impact analysis ;
- decision record ;
- roadmap ;
- external specs.

## 17. Gouvernance MayaBank

Cadence pédagogique :

```text
Monthly
- portfolio/lifecycle quality

Per architecture change
- target review
- dependency review

Quarterly
- technology standards
- obsolescence roadmap
```

## 18. KPI repository IT Architecture

```text
Object completeness
Relationship completeness
Owner coverage
Lifecycle freshness
Technology compliance
Legacy exit progress
Duplicate rate
```

## 19. Definition of Done

Une architecture MayaBank est `Done` quand :

- objets canoniques ;
- current et target ;
- relations critiques ;
- lifecycle ;
- standards ;
- impact analysis ;
- roadmap ;
- owner ;
- revue effectuée.

## 20. Entretien

**Quelle est la plus grande faiblesse d'un EAM ?**  
La qualité et la gouvernance insuffisantes des données, pas l'absence de diagrammes.

**Comment éviter un repository mort ?**  
En liant les données à des décisions récurrentes, des owners et des contrôles de fraîcheur.
