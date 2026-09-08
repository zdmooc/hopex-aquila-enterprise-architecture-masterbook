# 05 — Optimisation, simulation, process mining et automatisation

## 1. Le modèle doit conduire à une amélioration

Une Business Process Analysis utile ne s'arrête pas au diagnostic. Elle sert à identifier :

- bottlenecks ;
- étapes sans valeur ;
- rework ;
- handoffs ;
- contrôles redondants ;
- dépendances manuelles ;
- opportunités de standardisation ;
- opportunités d'automatisation ;
- risques de capacité ou de résilience.

## 2. Mesurer avant d'optimiser

Pour chaque amélioration, disposer d'une baseline :

```text
Cycle time
Waiting time
Error rate
Rework rate
Automation rate
Cost per case
STP rate
SLA breach rate
```

Sans baseline, l'amélioration est une opinion.

## 3. Value-added analysis

Classifier les activités :

- Value Added ;
- Business Necessary ;
- Non Value Added.

Exemple :

```text
Fraud Check          → Business Necessary
Manual duplicate key → Non Value Added
Customer confirmation→ Value Added / expected outcome
```

## 4. Bottleneck analysis

Un bottleneck peut venir de :

- capacité humaine ;
- système lent ;
- dépendance synchrone ;
- validation hiérarchique ;
- indisponibilité de données ;
- batch window ;
- handoff ;
- contrôle manuel.

Ne pas conclure automatiquement à « il faut automatiser ».

## 5. Process simulation

Le Store MEGA publie un **HOPEX Simulation Engine** étiqueté Business Process Analysis et compatible Aquila, avec des versions 62.x publiées en 2026.

La simulation peut servir à comparer des scénarios avec des hypothèses telles que :

- volume ;
- temps de traitement ;
- ressources ;
- probabilités de branches ;
- files d'attente ;
- capacité.

Les paramètres précis disponibles dépendent de la version/configuration et doivent être vérifiés dans l'environnement réel.

## 6. Exemple de scénario de simulation

Current :

```text
Manual Fraud Review
5 analysts
Average service time = 6 min
3% of payments routed to manual review
```

Target :

```text
Improved real-time scoring
1% routed to manual review
Same staffing
```

Comparer :

- queue length ;
- cycle time ;
- SLA breaches ;
- utilization.

Les chiffres du masterbook sont pédagogiques.

## 7. Process mining

Le process mining part des traces d'exécution réelles pour reconstruire ou analyser les chemins suivis.

Sources possibles :

```text
Case ID
Activity
Timestamp
Actor/System
Outcome
```

Exemple :

```text
PAY-123 | Validate | 10:00:00
PAY-123 | Fraud Check | 10:00:01
PAY-123 | Manual Review | 10:00:04
PAY-123 | Reject | 10:05:32
```

## 8. Model vs mined reality

```text
Designed process
≠
Observed process
```

Comparer :

- chemins non prévus ;
- loops ;
- activités contournées ;
- délais inattendus ;
- variantes locales ;
- non-conformance.

## 9. HOPEX et process mining

Le positionnement public de HOPEX BPM mentionne l'intégration avec des outils tiers de process mining pour accélérer l'analyse et la transformation.

Ne pas supposer qu'HOPEX remplace automatiquement un moteur de process mining spécialisé.

Architecture possible :

```text
Operational Logs
      ↓
Process Mining Tool
      ↓
Observed flows / metrics
      ↓
HOPEX repository
      ↓
Governed process model / target design
```

## 10. Automation candidates

Une activité est une candidate si :

- volume élevé ;
- règles stables ;
- données disponibles ;
- faible besoin de jugement humain ;
- bénéfice mesurable ;
- risque maîtrisable.

## 11. Types d'automatisation

### Workflow
Orchestration d'étapes et responsabilités.

### API
Automatisation d'échanges structurés.

### Event-driven
Réaction asynchrone à des événements.

### RPA
Automatisation d'interfaces existantes, souvent utile en transition mais à gouverner comme dette potentielle.

### Decision automation
Rules engine / fraud scoring / policy decision.

## 12. Process automation ≠ system architecture

Le modèle BPA exprime le besoin d'exécution.

L'architecture solution décide :

```text
BPM engine?
Microservices?
Event-driven?
Human task?
API orchestration?
RPA?
```

Ne pas faire de BPMN une architecture technique déguisée.

## 13. Continuous improvement loop

```text
Model
→ Execute
→ Measure
→ Mine / Observe
→ Analyze
→ Redesign
→ Govern
→ Execute again
```

## 14. Standardization

Avant optimisation locale :

- identifier variantes ;
- expliquer pourquoi elles existent ;
- distinguer contraintes réelles et habitudes ;
- définir un standard ;
- permettre exceptions explicitement gouvernées.

## 15. MayaBank — optimisation proposée

Current :

```text
Multiple synchronous checks
Manual repair after timeout
Point-to-point notifications
Poor end-to-end observability
```

Target :

```text
Idempotent orchestration
Real-time fraud decision
Explicit timeout/compensation
Event-driven status propagation
End-to-end trace correlation
```

## 16. Scorecard d'amélioration

| Dimension | Current | Target |
|---|---:|---:|
| STP | 96% | 99.5% |
| Manual repair | 2% | <0.2% |
| P95 duration | 4.5s | <2s |
| observability | fragmented | end-to-end |
| duplicate handling | manual | automated/idempotent |

Valeurs pédagogiques uniquement.

## 17. Anti-patterns

- automatiser avant de simplifier ;
- miner des logs sans case ID fiable ;
- comparer des KPIs aux définitions différentes ;
- confondre simulation et prédiction garantie ;
- utiliser RPA pour masquer une architecture cible absente ;
- optimiser localement une étape au détriment du cycle end-to-end ;
- ignorer le coût d'exploitation de l'automatisation.