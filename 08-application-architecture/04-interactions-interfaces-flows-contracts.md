# 04 — Interactions, interfaces, flux et contrats

## 1. Une dépendance applicative doit avoir une sémantique

Dessiner une flèche entre deux applications ne suffit pas.

Pour chaque interaction importante, documenter au minimum :

```text
Provider
Consumer
Purpose
Information exchanged
Direction
Interaction style
Criticality
Security expectation
Operational expectation
```

Puis ajouter protocole, endpoint, topic ou format si le niveau de décision l’exige.

## 2. Interaction vs interface vs flow

Dans ce masterbook :

### Interaction

Relation logique entre deux applications.

### Interface

Point contractuel exposé par un provider et consommé par un ou plusieurs consumers.

### Flow

Circulation d’une information ou d’un message entre participants.

Ces termes ne sont pas supposés correspondre automatiquement à trois métaclasses HOPEX identiques. Le métamodèle client fait foi.

## 3. Provider et consumer

Exemple :

```text
Provider
Fraud Decision Service

Interface
Fraud Decision API

Consumer
Payment Orchestrator
```

L’interface appartient conceptuellement au provider.

Le consumer dépend du contrat, pas de l’implémentation interne du provider.

## 4. Interface contract

Attributs utiles :

- name ;
- purpose ;
- provider ;
- consumers ;
- protocol/style ;
- version ;
- payload/information ;
- authentication ;
- authorization ;
- availability ;
- timeout ;
- idempotency ;
- deprecation date ;
- documentation link.

Ne pas recopier toute une spécification OpenAPI dans HOPEX si un catalogue API gouverné existe déjà.

## 5. REST / synchronous API

Exemple MayaBank :

```text
Payment Orchestrator
  |
  | HTTPS REST
  v
Fraud Decision Service
```

Points d’architecture :

- timeout ;
- retry ;
- idempotency ;
- circuit breaking ;
- authentication ;
- versioning ;
- latency budget ;
- error taxonomy.

## 6. Messaging

Exemple conceptuel :

```text
Payment Orchestrator
  → PaymentStatusChanged
  → Event Streaming
  → Notification Service
```

Documenter :

- producer ;
- consumer ;
- event/message ;
- topic/channel ;
- delivery expectations ;
- ordering ;
- replay ;
- retention ;
- schema governance.

Le repository EA ne remplace pas le schéma registry.

## 7. Batch / file exchange

Exemple :

```text
Reconciliation Service
→ settlement file
→ Finance Platform
```

Attributs utiles :

- schedule ;
- format ;
- volume ;
- encryption ;
- transfer protocol ;
- reconciliation/control ;
- recovery procedure.

Ne pas ignorer les flux batch sous prétexte qu’ils ne sont pas modernes.

## 8. Database coupling

Interaction dangereuse fréquente :

```text
Application A
→ direct SQL
→ Application B database
```

Questions :

- contrat explicite ?
- ownership des données ?
- impact de schema change ?
- sécurité ?
- transaction coupling ?
- plan de découplage ?

Le repository doit rendre ce couplage visible.

## 9. Shared database

Plusieurs applications peuvent utiliser une même base historique.

Ne pas masquer cette réalité.

Modéliser :

```text
Application A ─┐
               ├→ Shared Database
Application B ─┘
```

puis documenter la cible si la responsabilité data doit être séparée.

## 10. Protocol vs business semantics

`HTTPS` ne dit pas ce qui circule.

`PaymentInstruction` ne dit pas comment cela circule.

Conserver les deux niveaux :

```text
Business information
Payment Instruction

Technical transport
HTTPS/REST
```

## 11. Logical flow vs physical route

Vue logique :

```text
Payment Orchestrator
→ Fraud Decision Service
```

Vue physique possible :

```text
Payment Orchestrator
→ Service Mesh
→ API Gateway
→ Load Balancer
→ Fraud pods
```

Ne pas mélanger systématiquement les deux dans le même diagramme.

## 12. Interface ownership

Un contrat sans owner devient une dette.

Pour chaque interface critique :

- provider owner ;
- change approval ;
- version policy ;
- deprecation policy ;
- consumer communication ;
- support model.

## 13. Versioning

Exemple :

```text
Fraud Decision API v1
Fraud Decision API v2
```

Le repository doit permettre de savoir :

- quelle version est cible ;
- quels consumers utilisent encore l’ancienne ;
- date de retrait ;
- migration associée.

## 14. Backward compatibility

Une nouvelle version n’est pas automatiquement une nouvelle interface canonique.

Décider selon :

- rupture de contrat ;
- coexistence ;
- ownership ;
- cycle de migration ;
- besoin d’analyse.

## 15. Error semantics

Pour une interface critique, documenter au niveau architecture :

```text
Business reject
Technical retryable failure
Technical non-retryable failure
Timeout
Duplicate
Partial result
```

Cela aide à distinguer compensation métier et simple retry technique.

## 16. Timeout architecture

Une dépendance synchrone doit avoir un budget de temps.

Exemple :

```text
E2E payment target = 2 s
Fraud budget = 250 ms
Funds check = 200 ms
Clearing response = 900 ms
Other + network + orchestration = remaining budget
```

Chiffres pédagogiques.

## 17. Retry architecture

Un retry non gouverné peut amplifier une panne.

Documenter :

- retryable errors ;
- maximum attempts ;
- backoff ;
- idempotency ;
- dead-letter/repair strategy ;
- observability.

## 18. Idempotency

Pour les opérations financières :

```text
Same business request
+ same idempotency key
→ no duplicate financial execution
```

Le mécanisme exact appartient au design solution, mais l’exigence doit être visible.

## 19. Security context

Pour chaque interface sensible :

- identity propagation ;
- service authentication ;
- authorization ;
- encryption in transit ;
- secrets/certificate lifecycle ;
- sensitive payload classification ;
- audit requirements.

## 20. Application Flow Matrix MayaBank

| Provider | Consumer | Interaction | Style | Data |
|---|---|---|---|---|
| IAM | Digital Channel | Authentication | API | Auth Context |
| Payment Orchestrator | Digital Channel | Payment Status | API | Payment Status |
| Fraud Decision Service | Payment Orchestrator | Fraud Decision | API | Fraud Context/Decision |
| Core Account Service | Payment Orchestrator | Funds Check | API | Account/Funds |
| Clearing Gateway | Payment Orchestrator | Clearing Result | messaging/API | Payment/Clearing Result |
| Event Streaming | Notification Service | Status Event | event | Payment Status Changed |
| Notification Service | Customer Channels | Notification | multi-channel | Notification Request |

## 21. Interface criticality

Critères possibles :

- volume ;
- business criticality ;
- synchronous dependency ;
- data sensitivity ;
- number of consumers ;
- replacement difficulty ;
- regulatory impact.

## 22. Interface inventory quality

Questions :

1. chaque interface a-t-elle un provider ?
2. chaque consumer est-il connu ?
3. le contenu échangé est-il identifié ?
4. les versions sont-elles gouvernées ?
5. les flux critiques ont-ils un owner ?
6. les dépendances direct DB sont-elles visibles ?
7. les interfaces retirées sont-elles marquées ?

## 23. Anti-patterns

- toutes les flèches nommées `flow` ;
- protocole sans sémantique métier ;
- API sans provider clair ;
- consumer inconnu ;
- duplication d’une interface par diagramme ;
- interface versionnée sans politique de dépréciation ;
- dépendance SQL cachée ;
- Kafka topic assimilé automatiquement à un event métier ;
- message BPMN assimilé automatiquement à un message technique.

## 24. Livrables

- Application Interaction Diagram ;
- Interface Catalogue ;
- Provider × Consumer Matrix ;
- Critical Interface Register ;
- Direct DB Coupling View ;
- API/Event Migration View ;
- Interface Deprecation Plan.
