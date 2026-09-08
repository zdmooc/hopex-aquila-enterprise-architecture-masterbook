# 90 — Labs pratiques et questions corrigées

## 1. Labs

### Lab 01 — Data Domain Map
Construire les domaines Customer, Account, Payment, Fraud et Reference Data de MayaBank.

**Livrable :** Data Domain Map avec owner et périmètre.

### Lab 02 — Business Glossary
Créer 20 termes, dont Customer, Account, Payment Instruction, Payment Status, Fraud Decision et Clearing Result.

**Contrôle :** définition métier, owner, steward, domain, aliases et status.

### Lab 03 — Synonym & Homonym Review
Identifier cinq synonymes et trois homonymes potentiels. Définir le preferred term.

### Lab 04 — Conceptual Model
Construire Customer → Account → Payment → Fraud Decision → Clearing Result.

### Lab 05 — Logical Payment Model
Définir Payment, PaymentStatusHistory, FraudDecision et ClearingSubmission avec identifiers/cardinalities.

### Lab 06 — Physical Mapping
Mapper le logical model vers un schéma relationnel pédagogique sans mélanger les niveaux.

### Lab 07 — Inter-level Traceability
Relier Business Term → Conceptual Entity → Logical Attribute → Physical Column pour 10 CDEs.

### Lab 08 — Source-of-Truth Matrix
Identifier l’autorité pour Customer, Account, Payment, Fraud Decision et Reference Data.

### Lab 09 — Duplicate Authority Analysis
Traiter le conflit CRM/Core sur Customer Address.

### Lab 10 — Functional Lineage
Tracer Payment Instruction jusqu’à Notification, Reconciliation et Analytics.

### Lab 11 — Transformation Catalogue
Documenter au moins huit transformations avec source, rule/intention, target et owner.

### Lab 12 — Lineage Impact Analysis
Analyser l’impact d’un changement de sémantique de Payment Status.

### Lab 13 — Critical Data Elements
Sélectionner 12 CDEs et expliquer leur criticité.

### Lab 14 — Data Quality Rules
Définir 15 règles avec dimension, formule, threshold, owner et remediation.

### Lab 15 — Data Quality Incident
Simuler une hausse de Payment Status incohérents et conduire root-cause analysis via lineage.

### Lab 16 — Classification Map
Classifier les informations MayaBank selon Public/Internal/Confidential/Restricted pédagogique.

### Lab 17 — Privacy by Design
Réduire le payload de PaymentStatusChanged pour éviter les données client inutiles.

### Lab 18 — Retention Architecture
Construire une matrice catégorie/trigger/duration/rationale/owner sans inventer de durées réglementaires.

### Lab 19 — Store Architecture
Comparer relational DB, document, cache, event log, warehouse et object storage pour six use cases.

### Lab 20 — Shared Database Refactoring
Partir de trois applications lisant le même schema et construire une cible API/event-owned.

### Lab 21 — Data Contract
Définir PaymentStatusChanged v1 avec owner, schema, classification, compatibility et retention.

### Lab 22 — Current / Target
Construire la data architecture current et target du paiement instantané.

### Lab 23 — Migration & Reconciliation
Préparer un changement de Payment System of Record : profiling, backfill, delta, cutover, reconciliation, rollback.

### Lab 24 — Data Architecture Board
Préparer une synthèse : current, risks, sources of truth, target, data quality, privacy, lineage, roadmap.

---

# 2. Questions corrigées

### Q01 — Information et Data sont-ils synonymes ?
**Réponse :** Non. Information exprime le sens métier ; Data désigne une représentation de cette information.

### Q02 — Un Data Domain est-il une application ?
**Réponse :** Non. Le domaine représente une responsabilité sémantique durable, indépendamment de l’application qui l’implémente.

### Q03 — Pourquoi un Business Glossary ?
**Réponse :** Pour partager des définitions gouvernées et éviter synonymes, homonymes et interprétations concurrentes.

### Q04 — Business Term et column sont-ils équivalents ?
**Réponse :** Non. Un terme métier peut se matérialiser dans plusieurs attributs/columns et une column peut n’être qu’un détail technique.

### Q05 — À quoi sert le conceptual model ?
**Réponse :** À représenter les concepts et relations métier sans dépendance au DBMS ou à l’implémentation.

### Q06 — Que rajoute le logical model ?
**Réponse :** Entités, attributs, identifiants, cardinalités et règles structurelles, tout en restant indépendant du DBMS.

### Q07 — Que décrit le physical model ?
**Réponse :** Tables, columns, data types, indexes et autres choix d’implémentation d’une technologie précise.

### Q08 — Reverse engineering produit-il automatiquement un bon modèle métier ?
**Réponse :** Non. Il découvre la structure technique ; l’architecte doit contextualiser, nettoyer et relier aux concepts métier.

### Q09 — Data Owner et Data Steward ont-ils le même rôle ?
**Réponse :** Non. Owner porte l’accountability ; Steward maintient et anime la gouvernance opérationnelle.

### Q10 — Pourquoi identifier les Critical Data Elements ?
**Réponse :** Pour concentrer ownership, lineage, qualité et contrôles sur les données à fort impact.

### Q11 — Qu’est-ce que le functional lineage ?
**Réponse :** La traçabilité des informations et transformations dans leur contexte métier/applicatif.

### Q12 — Qu’est-ce que le technical lineage ?
**Réponse :** La traçabilité technique détaillée entre tables, columns, jobs, pipelines et transformations.

### Q13 — Pourquoi documenter une transformation ?
**Réponse :** Pour expliquer comment la donnée change et permettre impact analysis, audit et root-cause analysis.

### Q14 — Un simple diagramme d’applications constitue-t-il un lineage ?
**Réponse :** Non. Il faut au minimum savoir quelle information circule et comment elle est transformée.

### Q15 — Qu’est-ce qu’une dimension de Data Quality ?
**Réponse :** Un angle de qualité mesurable comme completeness, validity, uniqueness, consistency ou freshness.

### Q16 — Pourquoi ne pas mesurer toutes les colonnes pareil ?
**Réponse :** Les impacts diffèrent ; il faut prioriser CDEs et usages critiques.

### Q17 — Où corriger un défaut de qualité ?
**Réponse :** À la source autant que possible, tout en conservant des contrôles downstream appropriés.

### Q18 — Data observability et HOPEX sont-ils la même chose ?
**Réponse :** Non. HOPEX porte architecture/gouvernance/contexte ; la détection runtime peut être assurée par des outils spécialisés.

### Q19 — Classification et chiffrement sont-ils synonymes ?
**Réponse :** Non. Classification exprime la sensibilité ; chiffrement est un contrôle possible.

### Q20 — Retention et Backup sont-ils synonymes ?
**Réponse :** Non. Retention gouverne la durée de conservation ; backup répond surtout à la résilience/restauration.

### Q21 — Pourquoi la suppression doit-elle être analysée en lineage ?
**Réponse :** Parce que la donnée peut exister dans caches, replicas, analytics, exports et systèmes downstream.

### Q22 — Quelle différence Master Data / Reference Data ?
**Réponse :** Master Data représente des entités partagées durables ; Reference Data représente souvent des jeux de codes/classifications relativement stables.

### Q23 — Golden Record signifie-t-il « une table unique » ?
**Réponse :** Non. C’est une représentation maîtrisée issue d’un processus de gouvernance/matching/survivorship selon le contexte.

### Q24 — Toutes les duplications sont-elles mauvaises ?
**Réponse :** Non. Caches, replicas, read models et analytics peuvent être légitimes si authority et consistency sont claires.

### Q25 — Pourquoi le shared database est-il risqué ?
**Réponse :** Il crée coupling caché, ownership ambigu et blast radius lors des changements de schema.

### Q26 — Database per service est-il toujours préférable ?
**Réponse :** Non. Il augmente aussi la complexité de consistency, operations, reporting et reconciliation.

### Q27 — Event schema = enterprise logical model ?
**Réponse :** Non. Un event est un contrat contextualisé et temporel ; il doit être mappé aux concepts utiles.

### Q28 — Pourquoi versionner les data contracts ?
**Réponse :** Pour gouverner l’évolution et protéger producers/consumers contre les breaking changes.

### Q29 — Que signifie idempotency pour les données ?
**Réponse :** Un retry ou doublon ne doit pas produire plusieurs effets métier lorsque ce n’est pas souhaité.

### Q30 — CDC remplace-t-il un modèle d’intégration ?
**Réponse :** Non. CDC est un mécanisme ; ownership, semantics, consumers et schema evolution doivent rester gouvernés.

### Q31 — Source of Truth et System of Record sont-ils universellement définis ?
**Réponse :** Non. Les organisations les emploient différemment ; il faut expliciter la convention locale.

### Q32 — Qu’est-ce qu’un derived dataset ?
**Réponse :** Un dataset calculé ou projeté depuis une source autoritative, sans devenir automatiquement authoritative.

### Q33 — Pourquoi la reconciliation est-elle importante ?
**Réponse :** Elle détecte et traite les divergences entre sources/copies/systèmes distribués.

### Q34 — Que faut-il avant une migration data ?
**Réponse :** Profiling, mapping, quality baseline, consumer inventory, rehearsal et critères de reconciliation.

### Q35 — Quel est le risque du dual-write ?
**Réponse :** Partial failure, ordering et divergence entre deux cibles, donc besoin d’une stratégie explicite.

### Q36 — Quand un ancien store peut-il être retiré ?
**Réponse :** Quand consumers, retention, audit, historical needs et authority ont été traités et validés.

### Q37 — HOPEX doit-il contenir chaque table de production ?
**Réponse :** Non. Le niveau dépend de l’objectif d’architecture et de gouvernance ; le détail exhaustif peut rester dans des outils spécialisés.

### Q38 — Comment éviter un glossary graveyard ?
**Réponse :** Prioriser les termes critiques, leur ownership, leur usage et leurs relations avec processus/applications/data models.

### Q39 — Comment démontrer qu’une Data Architecture est utile ?
**Réponse :** Elle doit permettre de prendre des décisions d’impact, qualité, migration, source authority, sécurité et transformation.

### Q40 — Quelle question finale poser sur chaque donnée critique ?
**Réponse :** Qui en est responsable, où est l’autorité, qui la consomme, comment elle se transforme, et quel est l’impact si elle change ?
