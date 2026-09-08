# 09 — Labs et revue

## Labs

### Lab 01 — Définir le scope
Écrire la question de décision pour la capability map MayaBank Payments.

### Lab 02 — Construire L0/L1
Créer 8 à 10 domaines L0 puis 3 à 6 L1 par domaine.

### Lab 03 — Décomposer Payments
Construire L1/L2 et justifier chaque décomposition.

### Lab 04 — Revoir les noms
Transformer 15 faux noms de capabilities basés sur équipes, produits ou projets en aptitudes durables.

### Lab 05 — Définir les owners
Attribuer owner/steward à chaque capability du domaine Payments.

### Lab 06 — Strategic importance
Scorer 20 capabilities de 1 à 5 et justifier les cinq plus importantes.

### Lab 07 — Maturity model
Définir cinq critères observables pour `Instant Payment Execution`.

### Lab 08 — Current/Target
Évaluer 10 capabilities et calculer les gaps.

### Lab 09 — Heatmap
Construire une heatmap Importance × Gap et produire un top 5 d'investissement.

### Lab 10 — Capability × Application
Mapper Payment Orchestrator, Fraud Decision Service, Notification, Ledger, API Platform et Event Streaming.

### Lab 11 — Détecter la redondance
Identifier trois cas où plusieurs applications couvrent la même capability.

### Lab 12 — Détecter la sous-couverture
Identifier trois capabilities stratégiques dépendant d'un support IT insuffisant.

### Lab 13 — Capability × Data
Mapper Payment Instruction, Account, Customer Identity, Transaction et Settlement Status.

### Lab 14 — Capability × Technology
Identifier les dépendances technologiques critiques et les risques de lifecycle.

### Lab 15 — Capability × Initiative
Relier chaque gap prioritaire à une initiative ou signaler l'absence de réponse.

### Lab 16 — Scénarios
Comparer modernisation locale, plateforme cible et rationalisation forte.

### Lab 17 — Roadmap
Construire Current → Transition 1 → Transition 2 → Target pour Fraud Decisioning.

### Lab 18 — BIAN mapping
Créer un tableau de mapping entre un framework bancaire de référence et le modèle MayaBank sans recopier le framework.

### Lab 19 — Quality audit
Trouver 20 défauts dans une taxonomie volontairement mauvaise : doublons, niveaux incohérents, products-as-capabilities, owners absents.

### Lab 20 — Architecture Board
Présenter en 10 minutes : top gaps, applications impactées, risques technologiques, investissements proposés et outcomes.

## 30 questions corrigées

1. **Capability vs process ?** — Aptitude stable vs manière d'exécuter.
2. **Capability vs application ?** — Besoin métier durable vs moyen IT.
3. **Capability vs org-unit ?** — Aptitude vs responsabilité organisationnelle.
4. **Pourquoi une taxonomie ?** — Pour structurer et comparer les capabilities de manière cohérente.
5. **L3 est-il toujours nécessaire ?** — Non, seulement s'il sert une analyse ou décision.
6. **Pourquoi owner/steward ?** — Pour rendre la donnée gouvernable.
7. **Importance = maturity ?** — Non.
8. **Que représente current maturity ?** — Niveau actuel mesuré selon des critères définis.
9. **Que représente target maturity ?** — Niveau attendu pour satisfaire la stratégie.
10. **Pourquoi une heatmap ?** — Pour synthétiser des écarts et priorités.
11. **Une couleur est-elle une donnée ?** — Non, elle représente une donnée ou un score.
12. **Pourquoi mapper capability et application ?** — Pour analyser couverture, dépendances et rationalisation.
13. **Pourquoi mapper data ?** — Pour comprendre les dépendances informationnelles critiques.
14. **Pourquoi mapper technology ?** — Pour exposer obsolescence et risques techniques derrière une capability.
15. **Une application peut-elle supporter plusieurs capabilities ?** — Oui.
16. **Une capability peut-elle avoir plusieurs applications ?** — Oui.
17. **Pourquoi relier initiatives et gaps ?** — Pour vérifier que l'investissement répond à un besoin mesuré.
18. **Pourquoi séparer current et target ?** — Pour rendre explicite la transformation attendue.
19. **Qu'est-ce qu'un scénario ?** — Une option cohérente de transformation comparée à d'autres.
20. **Pourquoi définir des kill criteria ?** — Pour arrêter une initiative devenue non pertinente.
21. **BIAN remplace-t-il le capability model d'entreprise ?** — Non, c'est un modèle de référence.
22. **Peut-on importer un framework et l'adopter tel quel ?** — Techniquement possible selon outils, mais mauvaise gouvernance sans adaptation.
23. **Pourquoi tracer le mapping vers un framework ?** — Pour conserver provenance et comparabilité.
24. **Que signifie orphan application ?** — Application non reliée à une capability utile au modèle.
25. **Que signifie strategic gap without initiative ?** — Besoin prioritaire sans réponse de transformation identifiée.
26. **Pourquoi dater une assessment ?** — Parce qu'un score vieillit.
27. **Pourquoi éviter 'everything is strategic' ?** — Parce que le scoring ne priorise plus.
28. **Pourquoi éviter les micro-capabilities ?** — Elles déplacent le modèle vers le processus ou l'implémentation.
29. **Quel est le livrable exécutif principal ?** — Une vue synthétique importance/gap/investment/dependencies/outcomes.
30. **Quel critère prouve la maturité du dispositif ?** — Le lien continu Strategy → Capability → Assessment → Initiative → Outcome.

## Critère de maîtrise

La Partie VI est maîtrisée si l'architecte sait partir d'une stratégie, construire une taxonomie stable, l'évaluer, la relier aux moyens IT et produire une priorisation de transformation argumentée.