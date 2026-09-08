# 07 — Diagrams, Views & Matrices

## 1. Diagramme = représentation, pas vérité parallèle

Le principe de repository impose :

```text
Canonical objects
→ reused in diagrams
→ reused in lists
→ reused in reports
```

Un diagramme ne doit pas créer des copies sémantiques uniquement pour améliorer la mise en page.

## 2. Commencer par le concern

Avant toute vue :

```text
Stakeholder?
Question?
Decision?
Scope?
Time horizon?
```

Exemple :

> Le responsable Paiements veut savoir quelles applications supportent le processus Instant Payment et de quelles technologies critiques elles dépendent.

La vue doit répondre à cette question, pas montrer toute l'entreprise.

## 3. Vue applicative

Périmètre :

```text
Channel
→ API / integration
→ Payment Orchestrator
→ Fraud
→ Clearing Adapter
→ Notification
```

Ajouter uniquement les dépendances utiles au concern.

## 4. Vue technologique

```text
Applications
→ Platform services
→ Software technologies
→ hosting/runtime context
```

Ne pas dessiner tous les pods, IPs et instances si l'objectif est EA.

## 5. Vue cross-layer

```text
Capability
↓
Process
↓
Application
↓
Technology
↓
Transformation initiative
```

Très utile pour l'Architecture Board.

## 6. Matrice

Une matrice répond bien à des questions de couverture :

```text
Capabilities × Applications
Applications × Technologies
Processes × Applications
Applications × Owners
```

Elle est souvent meilleure qu'un diagramme lorsqu'il faut comparer beaucoup d'objets.

## 7. Diagramme vs matrice vs liste

```text
Diagram = structure / relations / flow
Matrix  = coverage / many-to-many comparison
List    = properties / review queue
Report  = aggregation / decision indicator
```

## 8. Règles de lisibilité

- un concern principal ;
- une légende si nécessaire ;
- limiter les croisements ;
- grouper selon une dimension explicite ;
- ne pas utiliser la couleur comme seule sémantique ;
- afficher le niveau de temporalité ;
- ne pas mélanger current et target sans distinction.

## 9. Layout vs semantics

Déplacer une boîte ne doit pas modifier le sens du repository.

Mais modifier une relation n'est jamais un simple changement graphique.

## 10. Diagramme de décision MayaBank

Question : retirer `Legacy Payment Gateway`.

Vue minimale :

```text
Capabilities affected
Processes affected
Consuming applications
Interfaces/flows
Target replacement
Technology dependencies
Migration initiative
```

## 11. Anti-patterns

- mega-diagram de 300 objets ;
- un diagramme par équipe avec copies ;
- couleurs sans légende ;
- relation dessinée visuellement mais non gouvernée ;
- diagramme utilisé comme base de données ;
- current/target superposés sans convention ;
- technologie produit représentée au mauvais niveau uniquement pour que "ça fasse architecture".

## 12. Lab

Pour MayaBank, définir :

1. une vue Executive ;
2. une vue Application Cooperation ;
3. une vue Technology Dependency ;
4. une matrice Capability × Application ;
5. une matrice Application × Technology.

Pour chaque représentation : stakeholder, concern, objets inclus, objets exclus et décision attendue.