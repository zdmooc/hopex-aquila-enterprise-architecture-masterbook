# 13 — Governance, Anti-Patterns & Mission Playbook

## 1. Objectif de gouvernance

Une bibliothèque de vues n’est pas un dossier de dessins.

Elle doit être gouvernée comme un produit d’architecture :

```text
standards
+ owners
+ review cycle
+ quality gates
+ usage
+ retirement
```

## 2. Rôles

### Enterprise Architect
Définit les standards cross-layer et la bibliothèque de vues.

### Domain Architect
Maintient les vues et relations de son domaine.

### Solution Architect
Produit les vues projet compatibles avec les objets canoniques.

### Repository Steward
Contrôle qualité, doublons, stale relations et conventions.

### Business/Data/Technology Owner
Valide les relations relevant de son périmètre.

## 3. Governance lifecycle

```text
Need identified
→ choose existing viewpoint/template
→ build scoped view
→ validate relationships
→ peer review
→ stakeholder review
→ approve/publish
→ monitor freshness
→ update or retire
```

## 4. Quality gate — relation

Une relation critique doit avoir :

- type correct ;
- endpoints canoniques ;
- direction cohérente ;
- source ;
- owner/règle d’ownership ;
- date ou fraîcheur adaptée ;
- confiance suffisante.

## 5. Quality gate — diagram

- stakeholder identifié ;
- concern explicite ;
- scope visible ;
- objets canoniques ;
- relations utiles seulement ;
- conventions conformes ;
- temporalité visible ;
- légende si nécessaire ;
- owner et statut.

## 6. Quality gate — matrix

- rows/columns définies ;
- relation type définie ;
- cellule vide interprétable ;
- scope/filters visibles ;
- taille maîtrisée ;
- source repository ;
- date si snapshot.

## 7. Quality gate — heatmap

- metric définie ;
- scale documentée ;
- source connue ;
- légende ;
- date ;
- alternative à la couleur.

## 8. Architecture Board review

Le board ne doit pas passer 30 minutes à déchiffrer un diagramme.

Pack recommandé :

```text
1. Concern & decision
2. Current view
3. Key dependency/impact view
4. Target/delta view
5. Matrix supporting the decision
6. Risks & assumptions
7. Decision requested
```

## 9. Metrics de gouvernance

Exemples :

```text
% published views with owner
% views reviewed on time
% critical relations verified
% duplicate views retired
% views using enterprise templates
% stale relations
% published views actually used
```

## 10. Anti-pattern — mega diagram

Symptôme :

```text
all enterprise objects on one canvas
```

Correction :

```text
landscape
→ domain view
→ dependency view
→ detail view
```

## 11. Anti-pattern — PowerPoint architecture

Symptôme : architecture modifiée dans le slide mais pas dans HOPEX.

Correction : repository first, communication artifact second.

## 12. Anti-pattern — semantic rainbow

Chaque couleur signifie quelque chose de différent selon la vue.

Correction : conventions globales et légendes obligatoires.

## 13. Anti-pattern — relation soup

Tous les liens sont `uses`, `depends on` ou `linked to` sans précision.

Correction : vocabulary contrôlé et review du métamodèle.

## 14. Anti-pattern — invisible scope

Une vue filtrée est présentée comme exhaustive.

Correction : afficher scope, filters, date et exclusions importantes.

## 15. Anti-pattern — duplicate truth

Même application représentée comme plusieurs objets dans plusieurs vues.

Correction : Search Before Create + canonical objects.

## 16. Anti-pattern — stale view

Une vue n’est jamais revue parce qu’elle « se génère encore ».

Correction : mesurer la fraîcheur des données et le besoin métier, pas seulement la capacité technique à l’ouvrir.

## 17. Anti-pattern — decorative relation

Une flèche est ajoutée pour rendre le diagramme logique visuellement mais ne correspond à aucun lien réel.

Correction : annotation graphique explicitement non sémantique ou relation réelle correctement modélisée.

## 18. Mission playbook — semaine 1

### Discover

- inventorier vues existantes ;
- identifier stakeholders ;
- identifier principales décisions ;
- revoir conventions ;
- échantillonner relations critiques ;
- détecter mega-diagrams et doublons.

Livrable : `Visual Architecture Assessment`.

## 19. Mission playbook — semaine 2

### Standardize

- définir relationship vocabulary ;
- définir view templates ;
- définir matrix templates ;
- définir visual grammar ;
- définir current/target convention ;
- définir quality gates.

Livrable : `View & Relationship Standard v1`.

## 20. Mission playbook — semaine 3

### Rebuild MayaBank-like pilot

- sélectionner un domaine ;
- corriger objets/relations ;
- produire landscape ;
- produire dependency view ;
- produire matrices ;
- produire target/delta ;
- publier au stakeholder.

Livrable : `Pilot Architecture View Pack`.

## 21. Mission playbook — semaine 4

### Industrialize

- créer view library ;
- attribuer owners ;
- créer review calendar ;
- définir metrics ;
- documenter publication ;
- former architectes et stewards.

Livrable : `Architecture Visualization Operating Model`.

## 22. Interview case — 300 applications

Question : « Le CIO veut une cartographie des 300 applications. »

Réponse :

1. clarifier la décision ;
2. produire un landscape L0/L1 ;
3. filtrer par domaine/criticality ;
4. utiliser matrices pour couverture ;
5. drill-down vers dépendances ;
6. ne jamais afficher 300 applications et toutes leurs relations sur une seule vue.

## 23. Interview case — application retirement

Livrables :

```text
Application context
Dependency impact view
Consumer/interface matrix
Technology dependencies
Target replacement
Transition view
Decision log
```

## 24. Interview case — technology obsolescence

```text
Deprecated technology
→ impacted platforms
→ applications
→ critical processes/capabilities
→ migration initiatives
```

Puis matrice Application × Technology et heatmap lifecycle.

## 25. Interview case — contradictory diagrams

Ne pas choisir le diagramme « le plus joli ».

Processus :

```text
compare canonical objects
→ compare relation sources
→ resolve repository truth
→ regenerate/rebuild views
→ archive obsolete views
```

## 26. Maturity model

### Level 1 — Drawings
Diagrammes isolés, copies, peu de gouvernance.

### Level 2 — Repository views
Objets partagés, relations structurées.

### Level 3 — Standardized
View library, matrices, conventions, owners.

### Level 4 — Analytical
Impact views, heatmaps, quality metrics, cross-layer navigation.

### Level 5 — Decision system
Vues self-service, gouvernance intégrée, usage régulier dans la transformation.

## 27. Definition of Done — Partie XI

Une organisation est prête pour la suite lorsque :

- les relations critiques ont une sémantique ;
- les vues sont scoped et owned ;
- les matrices sont gouvernées ;
- current/target est standardisé ;
- impact views sont reproductibles ;
- la publication ne crée pas de vérité parallèle ;
- les vues obsolètes peuvent être archivées ;
- l’Architecture Board utilise un pack cohérent.

## 28. Questions d’entretien

**Quel est le principal risque d’une stratégie de visualisation ?**  
Créer beaucoup de vues sans gouverner les objets et relations sous-jacents.

**Comment réduire la dette documentaire ?**  
Standardiser, réutiliser les objets canoniques, mesurer la fraîcheur et retirer les vues sans usage.

**Quel livrable est plus important : le diagramme ou le standard ?**  
Le standard et le repository permettent de produire durablement de bons diagrammes ; une image isolée ne suffit pas.