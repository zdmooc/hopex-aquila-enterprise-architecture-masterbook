# 11 — Publication, Collaboration, Hopex 360 & Audience Design

## 1. Une architecture utile doit être consommable

Un repository parfaitement modélisé mais invisible aux stakeholders crée peu de valeur.

La publication doit transformer :

```text
architecture data
→ understandable views
→ stakeholder access
→ review / feedback
→ decision
```

## 2. Publication ≠ duplication

Publier une vue ne doit pas créer une seconde source de vérité.

Le principe cible :

```text
Repository
→ governed view
→ portal / shared access
```

et non :

```text
Repository
→ screenshot
→ PowerPoint
→ copied spreadsheet
→ independent maintenance
```

## 3. Fait produit vérifié

Les pages publiques Bizzdesign Hopex de 2026 mettent en avant :

- reports, dashboards and enterprise portal ;
- self-service views for stakeholders ;
- un repository unifié ;
- Hopex 360 Viewer Portal dans la documentation contractuelle publique ;
- des cas clients utilisant Hopex 360 pour rendre modèles et diagrammes accessibles.

Les droits, rôles, licences et possibilités exactes dépendent du contrat et de la configuration client.

## 4. Audience segmentation

### Executive

Besoin : décisions, risques, investissement, trajectoire.

### Business owner

Besoin : capabilities, processes, applications support, risks.

### Enterprise architect

Besoin : cross-layer dependencies, standards, target state.

### Solution architect

Besoin : scoped design, interfaces, data, platforms, NFR.

### Operations / SRE

Besoin : critical dependencies, platform context, recovery.

## 5. One repository, multiple lenses

Exemple : `Payment Orchestrator`.

Executive :

```text
Strategic application / modernization enabler
```

Business :

```text
supports Execute Instant Payment
```

Solution :

```text
integrates Fraud/Core/Clearing
```

Technology :

```text
runs on OpenShift, uses PostgreSQL/Kafka
```

Même objet, vues différentes.

## 6. Portal landing page

Structure pédagogique :

```text
Business Architecture
Application Architecture
Data Architecture
Technology Architecture
Transformation
Risks
Key Decisions
```

## 7. Navigation path

Un bon parcours :

```text
Capability
→ Process
→ Application
→ Interface/Data
→ Technology
→ Initiative
```

La navigation est souvent plus utile qu’un PDF de 100 pages.

## 8. View description

Chaque vue publiée devrait indiquer :

```text
Purpose
Owner
Scope
Data date
Status
Audience
Known limitations
```

## 9. Draft vs approved

Éviter qu’une vue de travail soit interprétée comme architecture approuvée.

Statuts pédagogiques :

```text
Draft
Under Review
Approved
Superseded
Archived
```

Les statuts exacts doivent suivre la gouvernance client.

## 10. Review comments

Le feedback doit être transformé en correction du repository lorsque nécessaire.

Exemple :

```text
Comment: Fraud dependency missing
→ verify source
→ add/correct relationship
→ republish view
```

Pas seulement ajouter une annotation graphique.

## 11. Public vs restricted views

Une vue peut révéler :

- topology ;
- sensitive data ;
- security controls ;
- vendor vulnerabilities ;
- privileged infrastructure.

Les droits de publication doivent respecter la classification et le besoin d’accès.

## 12. Export

Exports utiles :

- Architecture Board pack ;
- audit evidence ;
- project documentation ;
- workshop material.

Mais l’export devient rapidement obsolète. Afficher une date de snapshot.

## 13. Screenshot governance

Une capture doit indiquer :

```text
Source: HOPEX
Snapshot: YYYY-MM-DD
View: <name>
```

pour éviter qu’elle soit réutilisée des mois plus tard comme vérité actuelle.

## 14. Executive storytelling

Ordre recommandé :

```text
Why
→ Current problem
→ Impact
→ Target direction
→ Decision required
```

Ne pas commencer par 50 applications.

## 15. Architecture Board storytelling

```text
Context
Current
Options
Target
Dependencies
Risks
Transition
Decision
```

## 16. MayaBank — portal lenses

### Payments Executive

- capability health ;
- modernization status ;
- top risks.

### Payments Architecture

- application cooperation ;
- data dependencies ;
- technology dependencies.

### Payments Transformation

- current/target ;
- migration waves ;
- decommission candidates.

## 17. Content freshness

Une vue publiée doit avoir :

- last reviewed ;
- owner ;
- source freshness ;
- status.

## 18. Usage analytics

Si disponible dans l’écosystème client, l’usage peut aider à identifier :

- vues réellement consultées ;
- contenus jamais utilisés ;
- stakeholders actifs.

Ne pas inventer une fonctionnalité HOPEX précise sans vérification.

## 19. Boundary with Part XV

Cette partie traite **comment publier une vue d’architecture**.

La Partie XV traitera en détail :

- reports ;
- dashboards ;
- KPIs ;
- aggregation ;
- decision support.

## 20. Anti-patterns

- portail rempli de vues sans audience ;
- publication de brouillons ;
- export sans date ;
- accès trop large à des vues sensibles ;
- PowerPoint maintenu indépendamment ;
- portail sans parcours de navigation ;
- aucune indication de fraîcheur.

## 21. Questions d’entretien

**Pourquoi publier depuis le repository ?**  
Pour maintenir un lien direct avec la connaissance canonique et réduire les copies divergentes.

**Pourquoi plusieurs audiences ?**  
Parce qu’un dirigeant, un business owner et un architecte solution n’ont ni les mêmes concerns ni le même niveau de détail.

**Quel risque avec un export ?**  
Il devient un snapshot statique qui peut rapidement diverger du repository.