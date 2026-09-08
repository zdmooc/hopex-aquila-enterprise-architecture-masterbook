# 02 — BPMN 2.0 : événements, activités, gateways et participants

## 1. Pourquoi BPMN

BPMN 2.0 fournit une notation standardisée pour représenter la logique d'un processus. HOPEX Business Process Management met explicitement en avant le support de BPMN 2.0.

Le but n'est pas d'utiliser tous les symboles disponibles, mais d'exprimer clairement le comportement utile à la décision.

## 2. Les familles fondamentales

### Events

Un événement représente quelque chose qui arrive.

Trois positions principales :

- Start Event ;
- Intermediate Event ;
- End Event.

Exemples MayaBank :

```text
Start Event       : Payment Request Received
Intermediate      : Clearing Response Received
End Event         : Payment Confirmed
```

### Activities

Une activité représente du travail.

```text
Validate Payment Request
Run Fraud Check
Reserve Funds
Send Clearing Message
Notify Customer
```

### Gateways

Une gateway sépare ou rejoint des chemins.

Utiliser une gateway lorsque le flux dépend réellement d'une règle ou d'une synchronisation.

### Sequence Flow

Ordre d'exécution au sein d'un même processus/pool.

### Message Flow

Communication entre participants/pools distincts.

## 3. Exclusive Gateway — XOR

Un seul chemin est choisi.

```text
Fraud decision?
├─ APPROVE → Continue
└─ REJECT  → Stop payment
```

Bonne pratique : nommer la décision comme une question et les branches comme des résultats.

Mauvais :

```text
Gateway G1
→ path 1
→ path 2
```

## 4. Parallel Gateway — AND

Plusieurs branches peuvent être exécutées en parallèle.

Exemple :

```text
Payment accepted
        ↓
       AND
      /   \
Update ledger   Prepare notification
      \   /
       AND
        ↓
Complete
```

Attention à ne pas l'utiliser pour une décision conditionnelle.

## 5. Inclusive Gateway — OR

Une ou plusieurs branches peuvent être prises selon conditions.

Elle est utile mais souvent mal comprise. Si le besoin peut être exprimé clairement avec XOR ou AND, rester simple.

## 6. Event-based Gateway

Le chemin dépend du premier événement reçu.

Exemple conceptuel :

```text
Wait for:
- clearing response
- timeout
```

C'est pertinent pour les systèmes distribués et processus asynchrones.

## 7. Pools et participants

Un pool représente un participant majeur au processus.

Exemple :

```text
Pool Customer
Pool MayaBank
Pool Clearing Network
```

Message flows entre pools.

Ne pas utiliser un pool pour chaque application technique si le diagramme vise le métier.

## 8. Lanes

Une lane aide à représenter une responsabilité au sein d'un pool.

Exemple :

```text
Pool MayaBank
  Lane Channel
  Lane Payments
  Lane Fraud
  Lane Operations
```

Une lane n'est pas automatiquement une Org-Unit canonique. La sémantique doit rester explicite.

## 9. Tasks et subprocesses

### Task

Travail atomique au niveau de détail choisi.

### Subprocess

Regroupe un ensemble d'activités réutilisable ou masque un niveau de détail.

Exemple :

```text
Execute Fraud Decision
```

peut être un subprocess contenant :

```text
Build Risk Context
→ Score Transaction
→ Apply Rules
→ Produce Decision
```

## 10. Call Activity

Permet de réutiliser un processus global défini séparément.

Utile pour :

- KYC shared process ;
- Notify Customer ;
- Manage Technical Incident ;
- Perform Compliance Check.

Éviter de copier le même sous-processus dans dix modèles.

## 11. Boundary Events

Un boundary event représente un événement attaché à une activité.

Exemple : timeout sur attente d'une réponse.

```text
Wait for Clearing Response
          │
       [Timer]
          ↓
Handle Clearing Timeout
```

Très utile pour documenter les exceptions techniques qui deviennent des exceptions métier.

## 12. Message Events

Dans une architecture événementielle, ne pas confondre :

```text
BPMN Message Event
≠ Kafka topic
≠ application event ArchiMate
≠ message ISO 20022
```

Le BPMN décrit le comportement du processus. Les objets techniques sont reliés séparément dans le repository.

## 13. Data Objects

Un Data Object BPMN représente une information consommée ou produite dans le contexte du processus.

Exemples :

- Payment Instruction ;
- Fraud Decision ;
- Clearing Result ;
- Customer Notification.

Ne pas transformer chaque colonne de base de données en Data Object BPMN.

## 14. Annotation et documentation

Une annotation peut clarifier une règle locale, mais les règles structurantes devraient devenir des objets gouvernés si elles doivent être réutilisées et analysées.

## 15. Happy path vs spaghetti

Commencer par le flux principal :

```text
Start
→ Validate
→ Decide
→ Execute
→ Confirm
→ End
```

Puis ajouter uniquement les exceptions importantes.

Un diagramme avec 80 exceptions devient illisible et doit être décomposé.

## 16. MayaBank — squelette BPMN logique

```text
Customer        MayaBank                         Clearing
   |               |                                |
   | Payment       |                                |
   |-------------->|                                |
   |               | Validate                       |
   |               | Fraud Check                    |
   |               | Funds Check                    |
   |               |-------------- Payment -------->|
   |               |                                |
   |               |<------------- Result ----------|
   |               | Update Status                  |
   |<--------------| Notify                         |
```

Ce squelette sera développé dans le modèle de référence de la Partie VII.

## 17. Anti-patterns BPMN

- gateway sans question métier ;
- activité nommée par un nom et non un verbe ;
- messages entre lanes alors qu'ils devraient être sequence flows ;
- pool par microservice ;
- données techniques partout dans une vue métier ;
- 100 activités sur un seul niveau ;
- absence de scénario d'exception pour les timeouts critiques ;
- modélisation de l'implémentation actuelle sans identifier la logique métier.

## 18. Checklist de revue BPMN

1. start/end explicites ;
2. activités avec verbes ;
3. gateways compréhensibles ;
4. responsabilités lisibles ;
5. message flow utilisé correctement ;
6. exceptions majeures représentées ;
7. data seulement si utile ;
8. niveau de granularité cohérent ;
9. subprocesses utilisés pour décomposer ;
10. diagramme compréhensible en moins de cinq minutes par un reviewer du domaine.