# 07 — Process Architecture : frontière avec la BPA

## 1. Pourquoi inclure les processus dans la Business Architecture

Les processus rendent les capabilities exécutables et contribuent à la réalisation des business services. La Business Architecture doit donc connaître les processus structurants sans nécessairement descendre au niveau BPMN détaillé.

```text
Capability
  ↓ enabled through
Process
  ↓ contributes to
Business Service
```

## 2. Process Architecture vs Process Model

Process Architecture :

```text
cartographie hiérarchique des processus
ownership
relations aux capabilities/services
performance/risk
```

Process Model :

```text
activities
sequence flows
events
gateways
roles
data
exceptions
```

La Partie VII traitera la BPA/BPMN détaillée.

## 3. Hiérarchie des processus

Exemple MayaBank :

```text
L1 Manage Payments
 ├─ L2 Execute Payment
 │   ├─ L3 Validate Payment
 │   ├─ L3 Decide Fraud
 │   ├─ L3 Route Payment
 │   └─ L3 Confirm Payment
 └─ L2 Operate Payments
     ├─ L3 Handle Exception
     └─ L3 Investigate Payment
```

Les niveaux doivent rester cohérents et gouvernés.

## 4. Process owner

Chaque processus important doit avoir un owner.

L'owner est responsable de :

- performance ;
- conformité ;
- amélioration ;
- documentation ;
- coordination des acteurs ;
- règles de contrôle.

## 5. Process × Capability

```text
Execute Instant Payment
→ Payment Orchestration
→ Fraud Decisioning
→ Payment Clearing
```

Cette relation permet de comprendre comment une aptitude est concrètement mise en œuvre.

## 6. Process × Business Service

```text
Execute Instant Payment
→ realizes/supports Instant Payment Service
```

La terminologie exacte de relation dépend du métamodèle HOPEX concerné ; le principe est de tracer la contribution du process au service.

## 7. Process × Application

Matrice utile :

| Process | Orchestrator | Fraud Engine | Ops Portal |
|---|---:|---:|---:|
| Validate Payment | X | X | - |
| Execute Payment | X | - | - |
| Handle Exception | X | X | X |

Permet de détecter :

- process critique sans support clair ;
- processus supporté par trop d'applications ;
- legacy hotspots ;
- impacts de retrait applicatif.

## 8. Process × Organization

```text
Process Owner
Process Performer
Control Owner
Support Role
```

Ne pas confondre ownership et exécution.

## 9. Process × Information

Exemple :

```text
Validate Payment
reads Payment Order
reads Customer Identity
produces Validation Result
```

Cela prépare le lineage business/data.

## 10. Performance

Indicateurs possibles :

- cycle time ;
- error rate ;
- straight-through rate ;
- rework ;
- cost ;
- compliance ;
- manual touch rate.

Un process map sans indicateur reste descriptif.

## 11. Risks & Controls

Exemple :

```text
Process: Execute Payment
Risk: duplicate execution
Control: idempotency + transaction state validation
```

Le niveau de détail GRC sera traité dans d'autres contextes, mais les points de contrôle importants doivent être traçables.

## 12. APQC et reference content

Le Store HOPEX propose un contenu APQC Cross Industry comprenant Process Map, catégories de processus, value streams/stages et performance indicators.

Ce contenu peut accélérer un projet, mais ne remplace pas l'adaptation à l'entreprise.

## 13. Current vs Target process architecture

Current :

```text
Manual validation
Batch clearing
Multiple handoffs
```

Target :

```text
Real-time validation
Automated decision
Event-driven confirmation
Exception-only manual handling
```

Le changement de process doit être relié aux capabilities, applications et initiatives.

## 14. Anti-patterns

- représenter chaque tâche comme un processus d'architecture ;
- processus sans owner ;
- processus décrits uniquement par l'application qui les supporte ;
- BPMN détaillé utilisé comme seule carte d'entreprise ;
- hiérarchie incohérente ;
- aucun lien avec capability/service ;
- process target sans métrique.

## 15. Entretien

**Pourquoi ne pas tout mettre en BPMN ?**  
Parce que l'EA a besoin d'une architecture de processus stable et navigable avant le détail d'exécution.

**Quelle relation est la plus importante ?**  
Le lien entre processus, capabilities, services et systèmes, car il rend l'impact analysis possible.