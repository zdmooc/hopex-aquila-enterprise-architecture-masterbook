# Partie XI — Relationships, Diagrams, Matrices & Views

Cette partie transforme le repository HOPEX en **système visuel de décision** : relations sémantiques, diagrammes, viewpoints, matrices, filtres, heatmaps, current/target, impact views, publication et gouvernance.

Elle approfondit les bases posées précédemment sans les répéter :

```text
Partie II
MetaAssociation / MetaAssociationEnd / cardinality

Partie III
UI, navigation, listes, diagrammes et matrices

Partie XI
sémantique, gouvernance et industrialisation des représentations

Partie XII
Enterprise Cartography & Dependency Analysis à grande échelle

Partie XV
Reports, Dashboards & Decision Support
```

Le fil rouge reste **MayaBank Instant Payment**.

---

# Objectifs

À la fin de cette partie, vous devez savoir :

- concevoir un vocabulary de relations ;
- distinguer relation directe et objet intermédiaire ;
- contrôler direction et sémantique ;
- gouverner source, evidence date et confidence ;
- détecter relations stale, conflicting et duplicate ;
- concevoir une vue à partir d’un stakeholder et d’un concern ;
- distinguer view et viewpoint ;
- choisir diagram vs matrix vs list ;
- définir des conventions visuelles ;
- construire matrices de couverture et CRUD ;
- utiliser filtres, scopes et queries ;
- concevoir heatmaps et overlays ;
- représenter Current / Transition / Target ;
- construire impact views et blast-radius analysis ;
- créer une bibliothèque de vues réutilisables ;
- publier des vues sans créer de vérité parallèle ;
- construire un Architecture Board pack ;
- auditer et retirer les vues obsolètes.

---

# Chapitres

## 01 — Rôle, périmètre et méthode

[Ouvrir](01-relationships-diagrams-matrices-views-role-scope-method.md)

Couvre :

- relationship > graphical line ;
- diagram = representation ;
- matrix = coverage ;
- view = concern + scope ;
- méthode en dix étapes ;
- niveaux Executive/EA/Solution/Detail.

## 02 — Relationship Semantics, Direction, Cardinality & Reification

[Ouvrir](02-relationship-semantics-direction-cardinality-reification.md)

Couvre :

- relation vocabulary ;
- direction ;
- symmetric/asymmetric ;
- hierarchy ;
- relation vs property/text ;
- objet intermédiaire ;
- interfaces ;
- business/app/data/risk/transformation relations.

## 03 — Relationship Governance, Evidence, Confidence & Data Quality

[Ouvrir](03-relationship-governance-evidence-confidence-quality.md)

Couvre :

- manual/imported/discovered/inferred ;
- source of truth ;
- confidence ;
- evidence date ;
- stale data ;
- contradictions ;
- duplicate/orphan relationships ;
- quality KPIs.

## 04 — Diagrams, Viewpoints, Stakeholders & Concerns

[Ouvrir](04-diagrams-viewpoints-stakeholders-concerns.md)

Couvre :

- stakeholder ;
- concern ;
- viewpoint ;
- Executive/Business/Application/Technology/Data/Risk/Transformation views ;
- scope ;
- drill-down ;
- storytelling.

## 05 — Visual Conventions, Layout, Labels & Readability

[Ouvrir](05-visual-conventions-layout-labels-readability.md)

Couvre :

- reading direction ;
- grouping ;
- color ;
- shapes ;
- lines ;
- labels ;
- accessibility ;
- legends ;
- current/target visual patterns.

## 06 — Matrices, Cross-References, Coverage & CRUD

[Ouvrir](06-matrices-cross-references-coverage-crud.md)

Couvre :

- binary/qualified matrices ;
- Capability × Application ;
- Process × Application ;
- Application × Technology ;
- CRUD ;
- Risk × Control ;
- Initiative × Capability ;
- matrix quality.

## 07 — Filters, Queries, Scoping & Derived Views

[Ouvrir](07-filters-queries-scoping-derived-views.md)

Couvre :

- filters ;
- relationship depth ;
- upstream/downstream ;
- current/target filters ;
- quality filters ;
- saved scopes ;
- query-driven analysis.

## 08 — Heatmaps, Overlays, Current/Target & Temporal Views

[Ouvrir](08-heatmaps-overlays-current-target-temporal-views.md)

Couvre :

- capability heatmap ;
- application health ;
- lifecycle overlay ;
- risk overlay ;
- delta view ;
- transition view ;
- temporal validity ;
- relationship-quality heatmap.

## 09 — Impact Views, Dependency Views & Blast Radius

[Ouvrir](09-impact-dependency-blast-radius-views.md)

Couvre :

- direct/transitive impact ;
- upstream/downstream ;
- critical path ;
- technology/data/risk/change impact ;
- failure domains ;
- cycles ;
- hubs ;
- blast radius.

## 10 — Reusable View Library, Templates & Architecture Standards

[Ouvrir](10-view-library-templates-architecture-standards.md)

Couvre :

- view templates ;
- naming ;
- mandatory enterprise views ;
- mandatory matrices ;
- visual grammar ;
- legacy diagram migration ;
- view retirement ;
- Architecture Board pack.

## 11 — Publication, Collaboration, Hopex 360 & Audience Design

[Ouvrir](11-publication-collaboration-hopex360-audience-design.md)

Couvre :

- publication without duplication ;
- Hopex 360 public evidence ;
- audience segmentation ;
- portal navigation ;
- draft/approved ;
- reviews ;
- security ;
- exports/snapshots ;
- storytelling.

## 12 — MayaBank Reference Model

[Ouvrir](12-mayabank-relationships-diagrams-matrices-reference-model.md)

Contient :

- canonical relationships ;
- current/target cooperation ;
- business/application/data/technology views ;
- critical dependency and failure-domain views ;
- transformation/delta views ;
- 8 matrices détaillées ;
- 12 vues de référence ;
- saved scopes ;
- quality/review rules.

## 13 — Governance, Anti-Patterns & Mission Playbook

[Ouvrir](13-governance-antipatterns-mission-playbook.md)

Couvre :

- roles ;
- lifecycle ;
- quality gates ;
- Architecture Board ;
- governance metrics ;
- mega-diagram ;
- PowerPoint architecture ;
- stale views ;
- mission quatre semaines ;
- interview cases ;
- maturity model.

---

# Pratique

## 90 — 24 labs + 40 questions corrigées

[Ouvrir](90-labs-and-review.md)

Labs :

1. Relationship Vocabulary.
2. Direction Review.
3. Reification Decision.
4. Relationship Evidence.
5. Stale Relationship Hunt.
6. Executive Viewpoint.
7. Application Cooperation View.
8. Technology Dependency View.
9. Visual Convention Standard.
10. Mega-Diagram Refactoring.
11. Capability × Application Matrix.
12. Process × Application Matrix.
13. Application × Technology Matrix.
14. CRUD Matrix.
15. Saved Scope.
16. Upstream / Downstream.
17. Technology Heatmap.
18. Relationship Quality Heatmap.
19. Current / Target Delta.
20. Legacy Gateway Blast Radius.
21. Kafka Failure View.
22. View Library.
23. Architecture Board Pack.
24. Governance Audit.

Puis **40 questions corrigées**.

---

# Sources

## 99 — Sources officielles & frontière de vérification

[Ouvrir](99-official-sources.md)

Sources principales vérifiées/recoupées en septembre 2026 :

- Bizzdesign Hopex current product pages ;
- Bizzdesign Hopex Service Level Agreement v20260123 ;
- Hopex 360 evidence ;
- Bizzdesign customer stories ;
- Bizzdesign technical-capabilities publication ;
- MetaAssociation/MetaAssociationEnd baseline déjà documentée en Partie II.

La source explique aussi pourquoi les fonctionnalités documentées sous **Horizzon Help** ne sont pas automatiquement attribuées à Hopex.

---

# Cas MayaBank — vues minimales

```text
V01 Executive Payment Transformation
V02 Capability × Application
V03 Process × Application
V04 Application Cooperation Current
V05 Application Cooperation Target
V06 Application × Data
V07 Application × Technology
V08 Critical Path / Failure Domains
V09 Risk × Control
V10 Current/Target Delta
V11 Transformation Waves
V12 Relationship Quality
```

---

# Règles à retenir

```text
Object ≠ Representation
Relationship ≠ Graphical line
Diagram ≠ Repository
View ≠ Viewpoint
Not shown ≠ Does not exist
Matrix cell ≠ Cosmetic edit
Discovered ≠ Verified
Current ≠ Target
Heatmap ≠ Metric definition
Many relations ≠ SPOF proof
Export ≠ Living source of truth
PowerPoint ≠ Architecture repository
```

---

# Chiffres de la Partie XI

- 13 chapitres complets ;
- 1 README de synthèse ;
- 1 modèle visuel MayaBank end-to-end ;
- 8 matrices détaillées dans le blueprint ;
- 12 vues MayaBank de référence ;
- 24 labs ;
- 40 questions corrigées ;
- sources produit séparées des pratiques recommandées ;
- frontière explicite Hopex vs Horizzon.

---

# Partie suivante

**Partie XII — Enterprise Cartography & Dependency Analysis**

Elle approfondira :

- enterprise landscapes ;
- dependency graph ;
- graph traversal ;
- upstream/downstream ;
- transitive dependencies ;
- criticality propagation ;
- clusters/hubs/cycles ;
- blast radius ;
- SPOF analysis ;
- change impact ;
- scenario analysis ;
- cartography governance à grande échelle.