# 12 — Labs & Review

## Objectif

Ces labs entraînent la navigation HOPEX comme une discipline de repository. Ils sont exécutables en mode documentaire sans licence et deviennent des labs UI réels dès qu’un environnement HOPEX est disponible.

---

## LAB 1 — Search before create

### Situation
On vous demande d’ajouter `Payment Orchestrator`.

### Travail
1. définir les variantes de nom à rechercher ;
2. identifier la MetaClass attendue ;
3. vérifier owner/domain/lifecycle ;
4. décider : réutiliser, corriger ou créer ;
5. documenter la décision.

### Critère de réussite
Aucun nouvel objet n’est créé tant que le risque de doublon n’est pas traité.

---

## LAB 2 — Object page quality review

Objet : `MayaBank Payment Orchestrator`.

Contrôler :

- nom canonique ;
- description ;
- owner ;
- lifecycle ;
- criticality ;
- source ;
- last review ;
- relations métier ;
- technologies majeures ;
- transformation target.

Produire une liste `OK / Missing / Questionable`.

---

## LAB 3 — Relationship navigation

Partir de `Payment Orchestrator` et construire :

```text
Application
→ Capability
→ Process
→ Interfaces
→ Data
→ Technology
→ Project
```

Pour chaque relation, préciser la question métier ou architecturale qu’elle permet de résoudre.

---

## LAB 4 — Capability impact

Question :

> Qu’est-ce qui supporte la capability Real-Time Payment Processing ?

Construire une table :

| Objet | Type | Rôle | Lifecycle | Criticality | Owner |
|---|---|---|---|---|---|

Puis identifier :

- dépendance unique critique ;
- redondance ;
- legacy ;
- cible.

---

## LAB 5 — Technology exit

Technology : `WebSphere`.

Construire :

```text
WebSphere
→ applications
→ processes/capabilities
→ owners
→ target platform
→ projects
```

Décider quelles informations doivent être visibles dans une vue Architecture Board.

---

## LAB 6 — List as data-quality control

Concevoir une liste logique :

```text
Applications
WHERE lifecycle IS NULL
OR owner IS NULL
OR lastReview < 12 months threshold
```

Ajouter :

- colonnes ;
- tri ;
- groupement ;
- action attendue.

---

## LAB 7 — Diagram by concern

Créer trois vues distinctes pour le même Payment Orchestrator :

1. business support ;
2. application integration ;
3. technology migration.

Interdiction de produire un diagramme unique fusionnant les trois concerns.

---

## LAB 8 — Current vs Target

Situation : migration WebSphere → OpenShift.

Séparer :

```text
CURRENT
Legacy Payment Gateway
→ WebSphere

TARGET
Payment Orchestrator
→ OpenShift

TRANSFORMATION
Modernization Initiative
```

Lister les données qui ne doivent pas être écrasées pendant la transition.

---

## LAB 9 — Architecture Board review

Préparer un pack minimal :

- concern ;
- scope ;
- current ;
- target ;
- impacts ;
- owner ;
- risks ;
- lifecycle ;
- roadmap ;
- decision requested.

Puis vérifier que chaque information provient d’objets/relations et non uniquement de texte libre.

---

## LAB 10 — Duplicate analysis

Jeu de données :

```text
Payment API
Payments API
Payment REST API
Instant Payment API
```

Construire une procédure de comparaison :

- type ;
- owner ;
- provider ;
- consumers ;
- external key ;
- documentation ;
- lifecycle.

Décider si ce sont quatre objets ou des doublons.

---

## LAB 11 — Workspace design

Créer un workspace conceptuel pour :

### Enterprise Architect
- critical applications ;
- capability gaps ;
- lifecycle alerts ;
- transformation initiatives ;
- validation queue.

### Application Owner
- owned applications ;
- incomplete properties ;
- upcoming review dates ;
- dependent interfaces.

### Platform Architect
- technology standards ;
- applications per technology ;
- obsolescence ;
- migration plans.

---

## LAB 12 — Collaboration workflow

Définir un processus complet de création d’une application :

```text
Draft
→ semantic review
→ owner validation
→ technology review
→ EA quality gate
→ publish
```

Pour chaque étape : acteur, entrée, contrôle, sortie.

---

## LAB 13 — Search strategy

Pour chaque terme, définir les recherches à tenter :

- OpenShift ;
- Kafka ;
- Instant Payment ;
- Fraud ;
- Payment Gateway.

Inclure : variantes, acronymes, external IDs, domains, owners.

---

## LAB 14 — Incident impact

Incident : `Event Streaming Platform unavailable`.

Construire la navigation d’impact :

```text
Technology Platform
→ dependent applications
→ interfaces/event flows
→ business processes
→ capabilities
→ critical owners
```

Classer impacts immédiats et indirects.

---

## LAB 15 — Green IT rationalization

Construire une liste candidate :

```text
Applications
WHERE lifecycle in {Tolerate, Eliminate}
AND business criticality != Critical
AND hosted on costly/legacy platform
```

Le modèle exact d’attributs dépendra de la solution HOPEX. Le lab teste le raisonnement.

---

# Questions de contrôle

1. Pourquoi rechercher avant de créer ?
2. Quelle différence entre objet et représentation ?
3. Pourquoi une vue n’est-elle pas le repository ?
4. À quoi sert un workspace par persona ?
5. Pourquoi owner et source sont-ils différents ?
6. Quand utiliser une liste plutôt qu’un diagramme ?
7. Pourquoi une relation structurée vaut-elle mieux qu’une description libre pour l’impact analysis ?
8. Pourquoi éviter les diagrammes monstres ?
9. Quelle différence entre current et target ?
10. Pourquoi ne pas écraser immédiatement le current lors d’une transformation ?
11. Que vérifie une Architecture Board review ?
12. Pourquoi un bulk edit est-il risqué ?
13. Que doit contenir une object page de qualité ?
14. Pourquoi les favoris ne remplacent-ils pas une taxonomie ?
15. Comment détecter un doublon ?
16. Comment suivre une technologie en fin de vie ?
17. Pourquoi une donnée synchronisée doit-elle encore être gouvernée ?
18. Pourquoi filtrer les CIs d’une CMDB avant exposition EA ?
19. Quel est le rôle d’une date de revue ?
20. Comment construire une impact analysis à partir d’un incident plateforme ?
21. Quel est le rôle de la criticité ?
22. Comment distinguer propriété et relation ?
23. Pourquoi documenter un filtre important ?
24. Pourquoi séparer contribution et validation ?
25. Quel est le risque d’une UI personnalisée avant clarification du métamodèle ?
26. Que doit faire l’architecte si un objet n’apparaît pas dans une vue ?
27. Pourquoi un repository sain nécessite-t-il des listes de contrôle qualité ?
28. Comment un owner utilise-t-il un workspace ?
29. Comment un platform architect navigue-t-il Technology → Applications ?
30. Pourquoi l’interface doit-elle rester une projection du repository ?

# Corrigé synthétique

1. Pour éviter les doublons et réutiliser l’objet canonique.
2. L’objet porte la donnée ; la représentation l’affiche dans un contexte.
3. Une vue ne montre qu’un sous-ensemble orienté concern.
4. Pour exposer les informations utiles à chaque responsabilité.
5. Owner = responsabilité ; source = origine autoritative de la donnée.
6. Pour inventorier, filtrer, comparer ou contrôler en volume.
7. Parce qu’elle est interrogeable et exploitable automatiquement.
8. Ils mélangent les concerns et deviennent illisibles.
9. Current décrit l’existant ; target la cible décidée.
10. Pour conserver la traçabilité de la transition.
11. Sémantique, impacts, ownership, current/target, risques et décision.
12. Une erreur se propage à de nombreux objets.
13. Identité, propriétés gouvernées, relations, source, owner, lifecycle et fraîcheur.
14. Ce sont des raccourcis personnels, pas une structure de gouvernance.
15. Comparer identité, type, source, owner, clés et relations.
16. Technology → applications → business impacts → target → projects.
17. L’automatisation ne décide pas des responsabilités ni des conflits.
18. Pour éviter de transformer HOPEX en CMDB bis.
19. Mesurer la fraîcheur et déclencher la revalidation.
20. Platform → applications → flows → processes → capabilities → owners.
21. Prioriser analyses, risques et transformation.
22. Propriété = valeur de l’objet ; relation = lien vers un autre objet.
23. Pour rendre l’analyse reproductible.
24. Pour instaurer un contrôle indépendant.
25. Créer des écrans qui figent une mauvaise sémantique.
26. Rechercher dans le repository et inspecter les relations.
27. Pour rendre les défauts visibles et actionnables.
28. Pour gérer les objets sous sa responsabilité et leurs revues.
29. En listant les consommateurs d’une technologie puis leurs dépendances métier.
30. Parce que la vérité doit rester dans les objets et relations canoniques.
