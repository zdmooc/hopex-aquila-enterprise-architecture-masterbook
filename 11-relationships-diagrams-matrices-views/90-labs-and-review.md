# 90 — Hands-on Labs & Review

Cette annexe contient **24 labs** et **40 questions corrigées** pour la Partie XI.

Les labs peuvent être préparés sur papier, Markdown ou draw.io lorsque HOPEX n’est pas disponible. Lorsque HOPEX est accessible, l’objectif est de reproduire la logique dans le repository avec les classes et relations réellement activées.

---

# Labs

## Lab 01 — Relationship Vocabulary

Construire un vocabulaire de 15 relations MayaBank :

```text
supports
owns
uses
consumes
produces
publishes
stores
runs on
implements
protects
mitigates
replaces
impacts
transforms
depends on
```

Pour chacune : définition, source, direction, exemples autorisés.

**Contrôle :** aucune relation générique `linked to`.

## Lab 02 — Direction Review

Prendre 20 relations du modèle Payments et vérifier :

- direction ;
- sens inverse ;
- libellé ;
- endpoints.

**Résultat attendu :** tableau `Correct / Suspect / Wrong`.

## Lab 03 — Reification Decision

Comparer :

```text
Application A → Application B
```

avec :

```text
Application A → Interface → Application B
```

Décider quand l’objet Interface est nécessaire.

**Contrôle :** l’objet intermédiaire doit porter des propriétés utiles.

## Lab 04 — Relationship Evidence

Pour 15 relations critiques, ajouter :

- source ;
- acquisition method ;
- evidence date ;
- confidence.

**Contrôle :** séparer `discovered` de `verified`.

## Lab 05 — Stale Relationship Hunt

Créer 10 relations dont certaines anciennes, puis définir un filtre permettant de trouver celles dépassant le seuil de revue.

**Contrôle :** expliquer pourquoi le seuil dépend du type de relation.

## Lab 06 — Executive Viewpoint

Construire une vue pour le Steering Committee :

```text
Payment modernization
Capabilities
Major applications
Top risks
Initiatives
```

**Exclure :** endpoints, topics, pods.

## Lab 07 — Application Cooperation View

Créer le flux cible :

```text
Channel
→ API Management
→ Payment Orchestrator
→ Fraud/Core/Clearing
→ Event Streaming
→ Notification/Reconciliation
```

**Contrôle :** toutes les flèches importantes ont un sens explicite.

## Lab 08 — Technology Dependency View

Pour `Payment Orchestrator`, représenter :

- OpenShift ;
- database ;
- IAM ;
- Event Streaming ;
- Observability ;
- network edge.

**Contrôle :** aucun pod individuel.

## Lab 09 — Visual Convention Standard

Définir :

- titre ;
- sens de lecture ;
- current/target ;
- labels ;
- légende ;
- annotation ;
- accessibility.

**Résultat attendu :** une page de standard.

## Lab 10 — Mega-Diagram Refactoring

Partir d’un diagramme conceptuel de 80 objets.

Le découper en :

1. L0 landscape.
2. L1 domain view.
3. L2 dependency view.
4. L3 solution detail.

**Contrôle :** chaque vue a un concern distinct.

## Lab 11 — Capability × Application Matrix

Construire la matrice Payments.

Analyser :

- gaps ;
- redundancy ;
- concentration.

**Contrôle :** définir ce que signifie une cellule vide.

## Lab 12 — Process × Application Matrix

Mapper les activités de `Execute Instant Payment` aux applications.

**Question :** quelles étapes dépendent de plusieurs applications critiques ?

## Lab 13 — Application × Technology Matrix

Construire une matrice :

```text
Applications × OpenShift/Kafka/Oracle/PostgreSQL/IAM/API Mgmt
```

Puis simuler `Kafka = Deprecated`.

**Contrôle :** identifier les applications à risque.

## Lab 14 — CRUD Matrix

Créer une CRUD matrix sur :

```text
Payment
Payment Status
Fraud Decision
Clearing Result
```

**Contrôle :** identifier le système maître de chaque donnée.

## Lab 15 — Saved Scope

Définir :

```text
PAYMENTS-CURRENT-PROD-CRITICAL
```

Critères : domaine, lifecycle, environment, criticality.

**Contrôle :** le scope doit être reproductible.

## Lab 16 — Upstream / Downstream

Sélectionner `Payment Orchestrator`.

Construire deux vues séparées :

```text
Upstream dependencies
Downstream consumers
```

**Contrôle :** ne pas mélanger les deux questions.

## Lab 17 — Technology Heatmap

Colorer conceptuellement les technologies selon :

```text
Preferred / Allowed / Deprecated / Unsupported
```

**Contrôle :** fournir aussi un label texte.

## Lab 18 — Relationship Quality Heatmap

Construire :

```text
Verified
Stale
Inferred
Missing source
```

sur une dependency view.

**Contrôle :** aucune conclusion d’impact sans mention du niveau de confiance.

## Lab 19 — Current / Target Delta

Créer :

```text
Keep
Change
Add
Retire
```

pour le Payment domain.

**Contrôle :** montrer `Legacy Payment Gateway = Retire` et `Payment Orchestrator = Add/Strategic`.

## Lab 20 — Legacy Gateway Blast Radius

Analyser :

```text
Legacy Gateway
→ consumers
→ interfaces
→ process activities
→ capabilities
→ technologies
→ initiatives
```

**Contrôle :** limiter l’analyse à deux niveaux puis justifier toute extension.

## Lab 21 — Kafka Failure View

Montrer l’impact d’une indisponibilité Event Streaming.

Distinguer :

- core financial path ;
- notification ;
- reconciliation ;
- analytics.

**Contrôle :** ne pas conclure que toute la transaction financière échoue si le modèle ne le prouve pas.

## Lab 22 — View Library

Créer un catalogue de 10 vues avec :

- owner ;
- audience ;
- purpose ;
- mandatory/optional ;
- review cycle.

## Lab 23 — Architecture Board Pack

Préparer :

1. Context.
2. Current.
3. Impact.
4. Target.
5. Key matrix.
6. Risks.
7. Decision requested.

**Sujet :** remplacement du Legacy Payment Gateway.

## Lab 24 — Governance Audit

Auditer 20 vues avec les critères :

```text
Owner
Status
Scope
Snapshot date
Template compliance
Relationship quality
Usage
Next review
```

Produire un backlog : `Keep / Fix / Merge / Retire`.

---

# 40 questions corrigées

## 1. Quelle est la différence entre un objet et sa représentation ?

**Réponse :** l’objet est canonique dans le repository ; sa représentation est l’occurrence visuelle utilisée dans une vue.

## 2. Pourquoi une relation est-elle plus importante qu’une flèche ?

**Réponse :** elle porte une sémantique réutilisable par navigation, matrices, APIs et analyses.

## 3. Pourquoi éviter `linked to` ?

**Réponse :** le lien est trop générique pour permettre une analyse fiable.

## 4. Quand créer un objet Interface ?

**Réponse :** lorsqu’il a une identité et des propriétés propres à gouverner : version, owner, protocol, lifecycle, SLA, etc.

## 5. Faut-il dupliquer la relation inverse ?

**Réponse :** non si le métamodèle représente une association navigable dans les deux sens.

## 6. À quoi sert la direction ?

**Réponse :** à distinguer producteur/consommateur, owner/owned, source/cible et autres rôles asymétriques.

## 7. Qu’est-ce qu’une relation `Verified` ?

**Réponse :** une relation confirmée par une source ou un owner faisant autorité selon la gouvernance définie.

## 8. `Discovered` veut-il dire `Verified` ?

**Réponse :** non. Une découverte technique doit souvent être interprétée et validée.

## 9. Pourquoi une evidence date ?

**Réponse :** parce qu’une relation peut devenir obsolète avec l’évolution du SI.

## 10. Qu’est-ce qu’un stale relationship ?

**Réponse :** une relation qui n’a pas été revue ou rafraîchie dans le délai attendu pour son type.

## 11. Qu’est-ce qu’un viewpoint ?

**Réponse :** un contrat de représentation définissant stakeholder, concern, contenu et règles de vue.

## 12. Qu’est-ce qu’une view ?

**Réponse :** une représentation concrète du repository appliquée à un scope et un concern.

## 13. Pourquoi plusieurs vues des mêmes objets ?

**Réponse :** pour répondre à plusieurs concerns sans dupliquer la vérité sémantique.

## 14. Quand utiliser un diagramme ?

**Réponse :** pour structure, flow, interactions et dépendances.

## 15. Quand utiliser une matrice ?

**Réponse :** pour couverture et comparaison many-to-many.

## 16. Quand utiliser une liste ?

**Réponse :** pour propriétés, triage, complétude et revue.

## 17. Pourquoi une cellule vide est-elle ambiguë ?

**Réponse :** elle peut signifier aucune relation, relation inconnue ou non collectée.

## 18. Quel est l’intérêt d’une CRUD matrix ?

**Réponse :** montrer qui crée, lit, met à jour et supprime une information afin de clarifier responsabilité et couplage.

## 19. Pourquoi limiter la taille d’une matrice ?

**Réponse :** pour conserver lisibilité et pertinence décisionnelle.

## 20. Pourquoi afficher le scope d’une vue ?

**Réponse :** pour qu’une vue filtrée ne soit pas interprétée comme exhaustive.

## 21. `Not shown` signifie-t-il `does not exist` ?

**Réponse :** non. L’objet peut être hors scope ou filtré.

## 22. Pourquoi limiter la profondeur d’une exploration ?

**Réponse :** chaque niveau supplémentaire ajoute bruit, complexité et risque de faux impacts.

## 23. Upstream et downstream répondent-ils à la même question ?

**Réponse :** non. Upstream = mes dépendances ; downstream = mes consommateurs/dépendants.

## 24. Qu’est-ce qu’une heatmap ?

**Réponse :** une vue qui applique une échelle visuelle à une propriété ou métrique pour mettre en évidence un état.

## 25. Pourquoi la couleur seule est-elle insuffisante ?

**Réponse :** accessibilité, impression, ambiguïté et perte de contexte.

## 26. Pourquoi dater une heatmap ?

**Réponse :** les valeurs de maturity, health, risk et lifecycle évoluent.

## 27. Qu’est-ce qu’une delta view ?

**Réponse :** une vue qui montre ce qui est conservé, modifié, ajouté ou retiré entre deux états.

## 28. Pourquoi le target ne suffit-il pas ?

**Réponse :** il ne décrit pas la trajectoire, les transitions, dépendances et risques de migration.

## 29. Qu’est-ce qu’un blast radius ?

**Réponse :** l’ensemble des objets et services susceptibles d’être affectés par un changement ou une panne.

## 30. Pourquoi le nombre de relations ne suffit-il pas à identifier un SPOF ?

**Réponse :** il faut connaître la nature des dépendances, les modes dégradés, la redondance et les chemins alternatifs.

## 31. Pourquoi un cycle de dépendances est-il intéressant ?

**Réponse :** il peut révéler couplage fort, shared state ou modélisation trop générique.

## 32. Qu’est-ce qu’une view library ?

**Réponse :** un catalogue gouverné de types de vues, templates et conventions réutilisables.

## 33. Pourquoi avoir un owner de vue ?

**Réponse :** pour garantir pertinence, fraîcheur, scope et maintien du standard.

## 34. Pourquoi archiver des vues ?

**Réponse :** pour éviter qu’un contenu obsolète continue d’être utilisé comme référence.

## 35. PowerPoint est-il interdit ?

**Réponse :** non. Il peut servir de support de communication, mais ne doit pas devenir une vérité architecturale indépendante.

## 36. Quel risque avec un screenshot ?

**Réponse :** il devient un snapshot statique facilement réutilisé hors contexte et hors date.

## 37. Que doit contenir un Architecture Board pack ?

**Réponse :** contexte, current, impact, target, matrice clé, risques et décision demandée.

## 38. Quel est le principal anti-pattern visuel ?

**Réponse :** vouloir tout montrer dans un seul mega-diagram.

## 39. Quel est le principal anti-pattern sémantique ?

**Réponse :** beaucoup de relations non définies, non sourcées et non maintenues.

## 40. Quelle est la règle d’or de la Partie XI ?

**Réponse :** une vue n’a de valeur durable que si elle projette des objets et relations canoniques, gouvernés et adaptés à une décision.