# 02 — Relationship Semantics, Direction, Cardinality & Reification

## 1. Pourquoi la sémantique des relations est critique

Un repository d’architecture devient puissant lorsqu’un lien signifie toujours la même chose.

Mauvais modèle :

```text
Application A -- linked to --> Application B
```

Bon modèle :

```text
Application A -- consumes --> Application Service B
Application A -- exchanges --> Payment Instruction -- with --> Application B
Application A -- deployed on --> Platform X
```

La précision permet analyses, matrices, requêtes et impact analysis fiables.

## 2. Relation directe

Une relation directe convient lorsque le lien lui-même ne nécessite pas de propriétés propres.

Exemple :

```text
Application
→ supports
Business Capability
```

## 3. Relation avec objet intermédiaire

Créer un objet intermédiaire lorsqu’il porte une identité ou des propriétés utiles.

Exemple :

```text
Application A
→ exposes
Interface Payment API v2
→ consumed by
Application B
```

L’interface peut porter :

- protocol ;
- version ;
- lifecycle ;
- owner ;
- SLA ;
- security classification ;
- payload ;
- deprecation date.

## 4. Direction

Une relation doit être lisible dans le sens principal et dans le sens inverse.

```text
Application → supports → Capability
Capability → supported by → Application
```

La direction graphique doit rester cohérente avec la direction sémantique choisie.

## 5. From / To n’est pas métier

Éviter de parler uniquement de `source` et `target` si la relation métier est claire.

Préférer :

```text
Producer → publishes → Event
Consumer → subscribes to → Event
Application → deployed on → Platform
Org Unit → owns → Application
```

## 6. Cardinalité

Les cardinalités exactes appartiennent au métamodèle activé et ne doivent pas être inventées.

Conceptuellement, elles aident à identifier :

```text
one owner
many supported capabilities
many consumers
optional replacement
```

Toute contrainte réelle doit être vérifiée dans le modèle client.

## 7. Symmetric vs asymmetric

Certaines relations sont asymétriques :

```text
Application A consumes Application B
```

D’autres peuvent être conceptuellement symétriques :

```text
Application A interoperates with Application B
```

Dans ce dernier cas, vérifier si une relation dédiée existe réellement avant de la créer.

## 8. Composition / aggregation

Ne pas utiliser composition ou agrégation uniquement pour obtenir un rendu hiérarchique.

La relation doit représenter une vraie structure :

```text
Application Suite
contains
Application Module
```

ou :

```text
Capability L1
is decomposed into
Capabilities L2
```

## 9. Parent / child

Les hiérarchies doivent être cohérentes :

```text
Payments
└─ Payment Execution
   └─ Instant Payment Execution
```

Anti-pattern : un objet ayant plusieurs parents incompatibles sans règle claire.

## 10. Relationship vocabulary

Taxonomie pédagogique MayaBank :

```text
supports
uses
owns
produces
consumes
exposes
implements
realizes
depends on
deployed on
stores
reads
writes
transforms
protects
mitigates
replaces
impacts
```

Les libellés HOPEX exacts doivent suivre le métamodèle installé.

## 11. Relation applicative

Exemple :

```text
Payment Orchestrator
→ invokes
Fraud Decision Service
```

À distinguer de :

```text
Payment Orchestrator
→ runs on
OpenShift Platform
```

Les deux relations portent des conséquences d’impact différentes.

## 12. Relation data

```text
Payment Orchestrator
→ creates/updates
Payment Status

Notification Service
→ reads
Payment Status
```

Une relation générique `uses data` perd l’information de responsabilité.

## 13. Relation risque / contrôle

```text
Duplicate Payment Risk
→ mitigated by
Idempotency Control
```

Puis :

```text
Idempotency Control
→ implemented by
Payment Orchestrator
```

Cette décomposition permet de distinguer risque, contrôle et implémentation.

## 14. Relation transformation

```text
Payment Modernization Initiative
→ impacts
Legacy Payment Gateway

Payment Modernization Initiative
→ delivers
Payment Orchestrator
```

Cela évite d’utiliser un simple commentaire de roadmap.

## 15. Relation temporelle

Quand la temporalité est importante, éviter d’encoder current/target uniquement dans le nom.

Préférer une propriété, un état, une date ou une vue dédiée selon le métamodèle.

## 16. Relation réciproque dupliquée

Mauvais :

```text
A → uses → B
B → used by → A
```

créées comme deux relations indépendantes.

Si le métamodèle représente une seule association navigable dans les deux sens, ne pas dupliquer.

## 17. Relation vs propriété

Si `Payments IT` est une Org Unit canonique :

```text
Application.Owner = relation vers Payments IT
```

est préférable à :

```text
OwnerName = "Payments IT"
```

lorsque l’analyse transverse est nécessaire.

## 18. Relation vs texte

Mauvais :

```text
Description = "Uses Kafka and PostgreSQL"
```

Meilleur :

```text
Application → uses → Kafka
Application → uses → PostgreSQL
```

## 19. Relation minimale utile

Créer une relation uniquement si :

- sa définition est claire ;
- sa source est connue ;
- elle répond à une question ;
- elle peut être maintenue ;
- elle ne duplique pas un lien plus précis.

## 20. MayaBank — exemple complet

```text
Real-Time Payment Capability
↑ supported by
Execute Instant Payment Process
↑ automated by
Payment Orchestrator
├─ consumes → Fraud Decision Service
├─ consumes → Core Account Service
├─ publishes → PaymentStatusChanged
├─ runs on → OpenShift Platform
└─ owned by → Payments IT
```

## 21. Checklist de revue

1. Relation autorisée par le métamodèle ?
2. Direction correcte ?
3. Libellé compréhensible ?
4. Source connue ?
5. Objet intermédiaire nécessaire ?
6. Relation redondante ?
7. Impact analysis utile ?
8. Relation maintenable ?

## 22. Questions d’entretien

**Quand créer un objet intermédiaire ?**  
Quand la relation possède une identité ou des propriétés qui doivent être gouvernées indépendamment.

**Pourquoi éviter `linked to` ?**  
Parce qu’une relation générique détruit la capacité d’analyse sémantique du repository.

**Pourquoi ne pas dupliquer les deux sens ?**  
Parce qu’une association correctement modélisée doit normalement être navigable depuis chacune de ses extrémités selon le métamodèle.