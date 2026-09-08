# 12 — Business Architecture Governance & Anti-patterns

## 1. Pourquoi la gouvernance est indispensable

Une Business Architecture peut devenir très vite incohérente si chacun crée ses propres capabilities, services, processus ou organisations.

La gouvernance doit donc porter sur :

- vocabulaire ;
- ownership ;
- niveaux de granularité ;
- règles de création ;
- règles de modification ;
- règles de déduplication ;
- source de vérité ;
- qualité ;
- publication ;
- cycle de revue.

## 2. Gouvernance par type d'objet

### Capability

- owner obligatoire pour les niveaux majeurs ;
- taxonomie contrôlée ;
- niveau explicite ;
- définition non liée à une application ;
- assessment method documentée.

### Value Stream

- stakeholder/value clairement défini ;
- stages limitées et cohérentes ;
- métriques si utilisées pour la décision ;
- liens vers capabilities/processes.

### Business Service

- consumer identifié ;
- business owner ;
- lifecycle ;
- supporting processes/capabilities.

### Process

- process owner ;
- hiérarchie ;
- mesure ;
- applications support ;
- risques/contrôles si pertinent.

### Organization

- source autoritative ;
- révision lors des réorganisations ;
- pas de duplication de personnes comme concepts permanents.

## 3. Naming conventions

Exemple :

```text
Capabilities : noun-based stable business ability
Processes    : verb + business object
Services     : value/service language
Org-Units    : official organization name
Initiatives  : transformation action name
```

Exemples :

```text
Capability : Payment Orchestration
Process    : Execute Instant Payment
Service    : Instant Payment Service
```

## 4. Repository Quality KPIs

```text
% capabilities with owner
% services with consumers
% processes with owner
% critical capabilities assessed
% capabilities linked to applications
% objects not reviewed > N months
suspected duplicates
orphan objects
```

## 5. Anti-pattern — Capability = Application

```text
Capability: Salesforce
Capability: SAP
Capability: Kafka
```

Pourquoi mauvais : la capability disparaît avec le produit.

Correction : identifier l'aptitude métier durable.

## 6. Anti-pattern — Capability = Org-Unit

```text
Capability: Payments Department
```

Correction :

```text
Org-Unit: Payments
Capability: Payment Orchestration
```

## 7. Anti-pattern — Process Map encyclopédique

Des milliers de processus sans hiérarchie ni owner deviennent inutilisables.

Correction : maintenir une process architecture à plusieurs niveaux et réserver le détail BPA aux processus qui le nécessitent.

## 8. Anti-pattern — Heatmap décorative

Toutes les capabilities sont colorées mais :

- aucune définition du score ;
- aucune source ;
- aucune date ;
- aucun owner ;
- aucune initiative.

Correction : chaque assessment doit supporter une décision.

## 9. Anti-pattern — View-driven repository

Créer un nouvel objet pour chaque diagramme conduit aux doublons.

Correction :

```text
Search
→ reuse canonical object
→ create representation
```

## 10. Anti-pattern — Strategy disconnected

Une capability map indépendante des objectifs ne dit pas où investir.

Correction :

```text
Objective
→ Capability
→ Assessment
→ Gap
→ Initiative
```

## 11. Anti-pattern — IT-first Business Architecture

```text
Applications
→ invent capabilities after the fact
```

Cette démarche peut être utile pour bootstrapper une carte, mais elle ne doit pas devenir la définition du métier.

Correction : valider les capabilities avec les stakeholders business.

## 12. Anti-pattern — Transformation without transition

```text
Current → Target
```

sans coexistence, ownership temporaire ni migration.

Correction : définir transition states et impacts opérationnels.

## 13. Anti-pattern — Uncontrolled customization

Créer une MetaClass ou propriété pour chaque notion locale augmente la dette du repository.

Correction :

1. vérifier le standard ;
2. privilégier classification/attribut existant ;
3. justifier l'extension ;
4. tester impacts UI/API/reporting ;
5. gouverner la version.

## 14. Architecture Board

Un board de Business Architecture doit challenger :

- scope ;
- stakeholder ;
- target outcome ;
- capability impact ;
- value impact ;
- ownership ;
- business/IT traceability ;
- gaps ;
- roadmap ;
- measures.

Il ne doit pas passer tout son temps à commenter le placement graphique des boîtes.

## 15. Change process

```text
Change request
→ impact analysis
→ owner review
→ architecture review if structural
→ update canonical objects
→ update assessments/views
→ publish
→ communicate
```

## 16. Quarterly review

Pour MayaBank :

```text
Review capabilities strategicity
Review maturity gaps
Review service ownership
Review process performance
Review organization changes
Review IT support changes
Review initiatives and outcomes
```

## 17. Definition of Done

Une modification de Business Architecture est complète si :

- objets canoniques utilisés ;
- owners connus ;
- relations utiles présentes ;
- sources définies ;
- vues concernées mises à jour ;
- impact downstream analysé ;
- décision/raison documentée ;
- aucune duplication introduite.

## 18. Entretien

**Quel est le risque majeur d'une Business Architecture dans un outil EAM ?**  
Accumuler des objets sans gouvernance jusqu'à perdre la confiance des utilisateurs.

**Comment éviter cela ?**  
Par des objets canoniques, ownership clair, taxonomies contrôlées, règles de qualité et un cycle de revue orienté décision.