# 12 — Labs & Review Questions

Cette partie propose des labs réalisables **sans redistribuer de logiciel ou contenu propriétaire HOPEX**. Les labs 1–6 sont documentaires/conceptuels ; les labs GraphQL deviennent exécutables lorsqu'un environnement HOPEX autorisé est disponible.

# LAB 01 — Construire un mini-métamodèle MayaBank

## Objectif

Définir un modèle minimal avant toute saisie HOPEX.

## Travail

Créer le tableau :

| Concept | Type prévu | Propriétés minimales | Relations |
|---|---|---|---|
| Capability | Business Capability | owner, maturity | process, app, initiative |
| Application | Application | owner, lifecycle, criticality | capability, technology |
| Technology | Software Technology | vendor, lifecycle | application |
| Org-Unit | Org-Unit | name, type | owns app/process |

## Validation

Pour chaque concept, expliquer :

- pourquoi il mérite une instance ;
- pourquoi il ne s'agit pas simplement d'un attribut ;
- quelle source le maintient.

---

# LAB 02 — MetaClass ou attribut ?

Classer les besoins suivants :

1. `Green IT Score` d'une Application ;
2. `Regulatory Obligation` réutilisée par plusieurs objets ;
3. `Criticality` ;
4. `Cloud Suitability` ;
5. `Payment Rail` ;
6. `Review Date` ;
7. `Technology Vendor`.

## Correction raisonnée

- Green IT Score : propriété/calcul dans la plupart des cas ;
- Criticality : propriété/classification ;
- Cloud Suitability : propriété/classification ;
- Review Date : propriété ;
- Regulatory Obligation : peut justifier un objet si le standard installé ne couvre pas déjà le concept et si elle porte relations/lifecycle ;
- Payment Rail : dépend de la sémantique et du métamodèle disponible ; ne pas créer une classe avant analyse ;
- Technology Vendor : souvent relation vers Vendor ou propriété selon modèle disponible.

---

# LAB 03 — Déduplication

Inventaire :

```text
Payment Orchestrator
PAY ORCH
Payment-Orchestrator
Payment Orchestrator PROD
Payment Orchestration Engine
```

Informations additionnelles :

```text
owner = Payments IT
external key = APP-483 pour 4 lignes
external key = APP-927 pour Payment Orchestration Engine
```

## Question

Combien d'objets canoniques ?

## Correction

Probablement deux :

```text
APP-483 → Payment Orchestrator
APP-927 → Payment Orchestration Engine
```

`PROD` ne doit pas créer un objet logique distinct sauf métamodèle de déploiement spécifique.

---

# LAB 04 — Source-of-truth matrix

Compléter :

| Donnée | Source maîtresse | HOPEX authority |
|---|---|---|
| Application logical identity | ? | ? |
| Server runtime CI | ? | ? |
| Capability | ? | ? |
| Cost center | ? | ? |
| Technology lifecycle | ? | ? |

## Proposition

```text
Application identity → HOPEX / app portfolio governance
Server CI → ServiceNow CMDB
Capability → HOPEX / EA governance
Cost center → Finance/ERP
Technology lifecycle → technology governance / HOPEX
```

La vraie réponse dépend de l'organisation.

---

# LAB 05 — Relation ou texte ?

Transformer :

```text
Description Application:
"Owned by Payments IT, uses Kafka and supports Real-Time Payment Processing."
```

En graphe :

```text
Application
→ owned by Org-Unit Payments IT
→ uses Event Streaming Technology
→ supports Real-Time Payment Capability
```

Puis expliquer pourquoi les relations sont meilleures pour l'analyse.

---

# LAB 06 — Capability hierarchy

Construire :

```text
Payments
├─ Initiation
├─ Validation
├─ Fraud Decision
├─ Execution
├─ Settlement
└─ Reconciliation
```

Puis ajouter :

```text
Application support
Owner
Maturity
Target maturity
```

Éviter une profondeur inutile.

---

# LAB 07 — GraphQL MetaModel query

À exécuter uniquement sur un environnement HOPEX autorisé.

```graphql
query {
  metaClass(filter: {name_starts_with:"Meta"}) {
    name
  }
}
```

Endpoint public documenté :

```text
/HOPEXGraphQL/api/MetaModel
```

## Vérifier

- authentification ;
- environment ID ;
- repository ID ;
- profile ID ;
- droits read-only ;
- présence de MetaClass/MetaAttribute/MetaAssociation.

---

# LAB 08 — Inspecter un schéma ITPM

Si l'environnement expose le schéma :

```graphql
query {
  application {
    id
    name
  }
}
```

Objectif : comprendre le mapping entre concept repository et champ GraphQL.

---

# LAB 09 — Contract test

Écrire un test conceptuel :

```text
Given ITPM schema
When schema is queried after upgrade
Then Application type still exists
And fields id/name exist
And required relationship fields exist
```

Ajouter les cas d'échec.

---

# LAB 10 — Change request de métamodèle

Demande :

> Créer une nouvelle MetaClass `CloudApplication`.

Produire une fiche de décision :

```text
Problem
Standard capability check
Alternative with attribute/classification
Impact UI
Impact API
Impact reports
Impact upgrade
Owner
Decision
```

La réponse recommandée est généralement de refuser la MetaClass si `Cloud` est seulement une caractéristique d'une Application.

---

# LAB 11 — Merge de doublons

Construire un runbook :

```text
Detect
→ Compare
→ Select canonical
→ Merge properties
→ Redirect relations
→ Validate diagrams/reports
→ Archive duplicate
→ Audit
```

---

# LAB 12 — MayaBank minimum viable repository

Créer sur papier/Markdown :

- 7 capabilities ;
- 5 processes ;
- 8 applications ;
- 6 technologies ;
- 5 org-units ;
- 4 initiatives.

Puis au moins :

- 20 relations Application→Capability ;
- 10 Application→Technology ;
- 8 owner relations ;
- 5 Project→Application.

Objectif : produire un graphe analysable, pas un inventaire plat.

---

# 30 questions de contrôle

1. Qu'est-ce qu'un MetaModel ?
2. Qu'est-ce qu'une MetaClass ?
3. Différence MetaClass / instance ?
4. Qu'est-ce qu'un MetaAttribute ?
5. Pourquoi utiliser une liste contrôlée ?
6. Qu'est-ce qu'une MetaAssociation ?
7. Pourquoi une association possède-t-elle des ends ?
8. Pourquoi ne pas utiliser le nom comme identité unique ?
9. Pourquoi un external key est-il utile ?
10. Pourquoi dédupliquer avant import ?
11. Différence hiérarchie / classification ?
12. Que confirme le template ITPM sur les capability maps ?
13. Pourquoi limiter la customisation ?
14. Quand une propriété custom suffit-elle ?
15. Quand une MetaClass custom peut-elle être justifiée ?
16. Quel rôle joue MetaStudio dans le workflow documenté du générateur GraphQL ?
17. À quoi sert `/api/MetaModel` ?
18. Quelles métaclasses techniques sont visibles dans l'exemple public ?
19. Pourquoi faire des contract tests après upgrade ?
20. Pourquoi ne pas importer toute la CMDB ?
21. Que signifie objet canonique ?
22. Quelle différence entre source, owner et steward ?
23. Pourquoi éviter les objets orphelins ?
24. Pourquoi une relation vaut mieux qu'un texte pour une dépendance ?
25. Que contient un registre de customisation ?
26. Pourquoi tester permissions et APIs après extension ?
27. Pourquoi séparer lifecycle et validation status ?
28. Qu'est-ce qu'un minimum viable record ?
29. Quelle première matrice MayaBank construire pour rationaliser les applications ?
30. Quelle est la règle d'or de cette partie ?

# Réponses synthétiques

1. Le modèle qui définit les concepts structurants du repository.
2. Un type d'objet du métamodèle.
3. Type vs objet réel.
4. Une propriété définie au niveau du métamodèle.
5. Pour fiabiliser saisie et reporting.
6. Une relation structurée entre concepts.
7. Pour donner du sens/navigabilité dans chaque direction.
8. Le nom peut changer et ne garantit pas l'unicité.
9. Pour synchroniser durablement avec une source externe.
10. Pour ne pas créer plusieurs vérités.
11. Parent/enfant vs axe de catégorisation.
12. Qu'une composition hiérarchique de business capabilities est un usage structuré supporté par le template officiel.
13. Coût upgrade, API, reporting, gouvernance.
14. Quand la nature de l'objet ne change pas.
15. Quand un concept durable absent du standard possède propriétés/relations/lifecycle propres.
16. Il permet de sélectionner/créer le fragment de métamodèle utilisé pour générer un mapping GraphQL.
17. Interroger le métamodèle exposé.
18. MetaClass, MetaAttribute, MetaAssociation, MetaAssociationEnd, etc.
19. Pour détecter les ruptures de schéma ou droits.
20. EAM et CMDB ont des granularités/finalités différentes.
21. Objet de référence unique d'une réalité gouvernée.
22. origine / responsabilité / maintenance qualité.
23. Ils ne permettent pas d'analyse de dépendance.
24. La relation est interrogeable et réutilisable.
25. raison, owner, type, version, impacts, migration.
26. Une extension peut casser des consommateurs.
27. Ce sont deux dimensions différentes.
28. Ensemble minimal de données fiables requis pour publier un objet.
29. Application×Capability, puis Technology/Owner/Lifecycle.
30. Un bon repository est plus important qu'un beau diagramme.
