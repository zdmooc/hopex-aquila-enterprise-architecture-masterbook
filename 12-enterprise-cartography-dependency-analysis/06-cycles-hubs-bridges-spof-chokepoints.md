# 06 — Cycles, Hubs, Bridges, SPOF & Architectural Choke Points

## 1. Pourquoi analyser la structure du graphe

La cartographie ne sert pas seulement à suivre des dépendances. Elle permet aussi d’identifier des **formes structurelles de risque** :

- cycles ;
- hubs ;
- dépendances partagées ;
- bridges ;
- choke points ;
- single points of failure logiques ;
- objets isolés ;
- chemins excessivement longs.

Ces concepts sont des méthodes d’analyse de graphe. Le masterbook ne prétend pas que tous sont exposés comme calculs natifs dans Hopex.

---

## 2. Cycle

Un cycle existe lorsque l’on peut revenir au point de départ en suivant une chaîne de dépendances.

Exemple :

```text
Application A
→ Application B
→ Application C
→ Application A
```

---

## 3. Pourquoi un cycle peut être problématique

Il peut révéler :

- couplage fort ;
- dépendances d’initialisation ;
- ordre de démarrage ambigu ;
- difficulté de test ;
- difficulté de migration ;
- risque de cascade ;
- ownership partagé confus.

Un cycle n’est pas automatiquement mauvais ; il doit être compris.

---

## 4. Cycle fonctionnel vs technique

### Fonctionnel

```text
Process A needs Process B result
Process B needs Process A state
```

### Technique

```text
Service A calls B
B calls C
C calls A
```

Les remédiations sont différentes.

---

## 5. Strongly connected component — concept

Un ensemble fortement connecté correspond à un groupe où chaque nœud est atteignable depuis les autres dans le sens des relations.

Pratique utile pour repérer un cluster de couplage.

Exemple pédagogique :

```text
Legacy Payment Hub
Legacy Fraud Adapter
Legacy Notification Gateway
Shared Database
```

Si les dépendances forment un noyau fortement couplé, une migration par application isolée devient difficile.

---

## 6. Hub

Un hub est un objet avec beaucoup de connexions importantes.

Exemples possibles :

```text
IAM Platform
API Management
Event Streaming
Shared Database
Core Banking Service
```

Le degré élevé ne suffit pas à conclure que le hub est risqué.

---

## 7. In-degree et out-degree — concepts

### In-degree

Nombre de relations entrantes selon une sémantique donnée.

Exemple : nombre de consommateurs d’une API.

### Out-degree

Nombre de dépendances sortantes.

Exemple : nombre de services externes appelés par une application.

Ces métriques sont utiles pour détecter concentration et couplage.

---

## 8. Hub métier

Une application supportant beaucoup de processus peut être un hub métier.

```text
Core Account Service
→ many payment/account processes
```

---

## 9. Hub technique

```text
IAM Platform
→ many applications
```

ou :

```text
Kafka Platform
→ many producers and consumers
```

---

## 10. Shared dependency

Un hub partagé est important car une panne peut toucher plusieurs domaines.

```text
Payments ─┐
Fraud ────┼→ IAM
Customer ─┘
```

---

## 11. Bridge — concept

Un bridge est une relation dont la suppression sépare des portions du graphe.

Exemple pédagogique :

```text
Internal Payments
→ Clearing Gateway
→ External Clearing Network
```

Si le Clearing Gateway est la seule connexion entre les deux mondes, il constitue un bridge architectural.

---

## 12. Articulation point — concept

Un nœud d’articulation est un objet dont la perte peut séparer une partie du graphe.

Exemple :

```text
All partner traffic
→ one integration gateway
```

Il peut devenir un point de concentration majeur.

---

## 13. SPOF logique

Un single point of failure logique existe lorsqu’un service dépend d’un élément unique sans alternative fonctionnelle ou technique suffisante.

Exemples :

```text
Single IAM tenant
Single clearing adapter
Single shared DB schema
Single DNS dependency
Single certificate authority path
```

---

## 14. SPOF logique ≠ instance unique

Une plateforme peut avoir plusieurs instances mais rester un SPOF logique.

Exemple :

```text
3 IAM replicas
but one logical IAM service
with one configuration/control plane failure mode
```

La redondance physique doit être analysée avec les failure modes.

---

## 15. Choke point

Un choke point est un passage obligatoire concentrant flux ou dépendances.

Exemple :

```text
All external payments
→ one API gateway cluster
```

Même si hautement disponible, ce point mérite :

- capacity analysis ;
- HA ;
- DR ;
- security review ;
- monitoring ;
- ownership clair.

---

## 16. Bottleneck vs choke point

### Bottleneck

Limitation de capacité/performance.

### Choke point

Passage architectural obligé.

Un choke point peut devenir bottleneck, mais les deux concepts ne sont pas identiques.

---

## 17. Shared database as coupling hub

```text
App A ─┐
App B ─┼→ Shared Database
App C ─┘
```

Risques :

- schema coupling ;
- change coordination ;
- blast radius ;
- access control complexity ;
- migration difficulty.

---

## 18. API gateway as controlled hub

Un hub n’est pas nécessairement un anti-pattern.

API Management peut volontairement centraliser :

- authentication ;
- policies ;
- rate limiting ;
- observability ;
- exposure control.

La question devient : le hub est-il résilient et gouverné ?

---

## 19. Event platform hub

Kafka/Event Streaming peut devenir une dépendance transverse.

Analyser :

- producers ;
- consumers ;
- critical topics ;
- schema dependencies ;
- replay ;
- cluster failure modes ;
- capacity under failure.

---

## 20. IAM hub

Analyser :

```text
Human identity
Service identity
Token issuance
Federation
Privileged access
Certificate dependencies
```

Une panne IAM peut avoir un blast radius supérieur à celui visible dans une simple application map.

---

## 21. Network choke point

Exemples :

- unique firewall path ;
- unique WAN link ;
- single DNS zone ;
- unique ingress layer ;
- single partner tunnel.

À relier aux services consommateurs.

---

## 22. Organizational SPOF

Une seule personne ou équipe peut détenir :

- compétence vendor rare ;
- droits de production ;
- clé de récupération ;
- procédure manuelle critique.

Le repository peut au minimum relier ownership et services critiques.

---

## 23. Vendor concentration

```text
Many critical platforms
→ one provider
```

Cette dépendance peut être commerciale/contractuelle autant que technique.

---

## 24. Cycle detection workshop

Méthode :

1. choisir un domaine ;
2. filtrer relations runtime/applicatives ;
3. rechercher boucles ;
4. confirmer avec owners ;
5. identifier cause ;
6. décider si le cycle doit être accepté ou réduit.

---

## 25. Hub review workshop

Pour un hub :

```text
Consumers?
Critical consumers?
Fallback?
HA?
DR?
Capacity?
Owner?
Lifecycle?
Change process?
```

---

## 26. MayaBank — hubs de référence

Potentiels hubs pédagogiques :

```text
API Management
IAM Platform
Event Streaming
Core Account Service
Observability Platform
```

Ils ne sont pas automatiquement des SPOF.

---

## 27. MayaBank — legacy cycle

Exemple pédagogique :

```text
Legacy Payment Hub
→ Shared Payment DB
→ Legacy Reconciliation Batch
→ Payment Status Update
→ Legacy Payment Hub
```

Un cycle de données/traitement peut compliquer la décomposition.

---

## 28. MayaBank — bridge clearing

```text
Internal payment domain
→ Clearing Gateway
→ External Clearing Service
```

Si aucun second mécanisme n’existe, le gateway est un bridge critique entre domaines.

---

## 29. Risk register pour concentration

| Pattern | Object | Risk | Evidence | Mitigation |
|---|---|---|---|---|
| Hub | IAM | broad outage | dependency map | multi-site + DR |
| Bridge | Clearing Gateway | external isolation | interface map | resilience + fallback |
| Cycle | Legacy Payment chain | migration coupling | workshops | decouple events/data |
| Shared DB | Payment DB | schema blast radius | DB mapping | ownership/refactor |

---

## 30. Anti-patterns

- degree élevé = SPOF automatique ;
- plusieurs replicas = absence de SPOF ;
- cycle supprimé uniquement du diagramme ;
- hub non documenté parce qu’il est « standard » ;
- shared DB considéré seulement comme stockage ;
- bridge ignoré car externe ;
- concentration organisationnelle absente de l’analyse.

---

## 31. Questions d’entretien

**Qu’est-ce qu’un hub ?**  
Un objet concentrant de nombreuses relations importantes ; il mérite une analyse de blast radius et de résilience.

**Qu’est-ce qu’un SPOF logique ?**  
Un service ou mécanisme unique dont la perte bloque une fonction, même s’il est techniquement répliqué.

**Pourquoi un cycle est-il important pour une migration ?**  
Parce qu’il révèle un couplage qui peut empêcher de déplacer ou retirer un composant indépendamment.

**Bridge et bottleneck sont-ils identiques ?**  
Non. Le bridge structure la connectivité ; le bottleneck limite la capacité ou performance.
