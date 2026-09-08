# 06 — Identity, Naming, Keys & Deduplication

## 1. Le problème de l'identité

Un repository EAM échoue vite si la même réalité est représentée plusieurs fois.

Exemple :

```text
Payment Orchestrator
Payment Orchestration
Payment-Orchestrator
PAY ORCH
Orchestrator Prod
```

Peut-être cinq objets. Peut-être une seule application.

## 2. Nom vs clé

Le nom doit être lisible par les humains.

La clé doit permettre de retrouver durablement l'objet.

```text
Display name = Payment Orchestrator
Canonical key = APP-PAY-002
External key = valeur provenant d'une source maîtresse
```

Le nom peut changer ; l'identité ne devrait pas changer pour cette raison.

## 3. Identifiants HOPEX

HOPEX gère ses propres identifiants techniques d'objets. Les détails exacts de comportement des identifiants internes/externes doivent être validés dans la version et l'API cible avant de concevoir une synchronisation.

Le masterbook applique donc cette règle :

```text
Never design integration around display name alone.
```

## 4. Clé canonique MayaBank

Convention pédagogique :

```text
CAP-PAY-001  Capability
BPR-PAY-001  Business Process
APP-PAY-001  Application
TEC-PLT-001  Technology / Platform
ORG-PAY-001  Organization
DAT-PAY-001  Data concept/domain
```

Cette clé est pédagogique ; elle ne remplace pas les identifiants HOPEX natifs.

## 5. Déduplication avant import

Avant chargement massif :

```text
normalize
→ exact match on external key
→ canonical key match
→ normalized name match
→ contextual match
→ human review for ambiguous cases
```

## 6. Normalisation

Exemples :

```text
trim spaces
normalize case
remove accidental punctuation
normalize known abbreviations
preserve business-significant differences
```

Attention : normaliser ne signifie pas fusionner automatiquement.

`Payment Hub` et `Payment Orchestrator` peuvent être deux objets réellement différents.

## 7. Matching multi-critères

Pour une Application :

```text
external key
+ name
+ owner
+ domain
+ source system
+ lifecycle
```

Une similarité de nom seule n'est pas suffisante.

## 8. Golden record

Quand deux objets sont doublons :

1. choisir le record canonique ;
2. comparer les propriétés ;
3. choisir la source maîtresse par champ ;
4. déplacer/recréer les relations sur le canonique ;
5. vérifier vues/rapports ;
6. archiver le doublon ;
7. supprimer seulement si le processus le permet.

## 9. Collision de clés

Une clé externe peut n'être unique que dans une source donnée.

Mieux :

```text
source_system + source_object_type + external_key
```

Exemple :

```text
SERVICENOW | APPLICATION | A12345
ERP        | COSTCENTER  | A12345
```

## 10. Rename

Un rename ne doit pas créer un nouvel objet.

```text
Payment Hub v1 renamed to Instant Payment Platform
```

Si l'identité métier reste la même :

```text
same object
+ new display name
+ history/audit if supported
```

## 11. Split et merge

Plus complexe :

```text
Legacy Payment Hub
→ split into
Payment Orchestrator
Clearing Adapter
Notification Service
```

Ici il s'agit réellement de nouveaux objets et d'une transformation, pas d'un simple rename.

## 12. Naming rules

Une convention utile :

- nom métier compréhensible ;
- pas de nom d'environnement dans l'objet logique ;
- pas de version dans le nom sauf si la version constitue réellement un objet distinct ;
- éviter les acronymes locaux non documentés ;
- pas de préfixe technique inutile ;
- nom stable entre vues.

## 13. MayaBank — exemples

### Bon

```text
Payment Orchestrator
Fraud Engine
Event Streaming Platform
Customer Notification Service
```

### Mauvais

```text
APP_001_NEW
PO PROD
Kafka2
Payment Service Final v3
```

## 14. KPI qualité

- doublons confirmés ;
- doublons suspects ;
- objets sans clé externe alors qu'ils viennent d'une intégration ;
- clés externes en collision ;
- noms hors convention ;
- objets sans source.

## 15. Entretien

**Comment évitez-vous les doublons ?**  
Par identité canonique, clés externes, recherche avant création, matching multi-critères et workflow de fusion.

**Pourquoi ne pas utiliser le nom comme identifiant ?**  
Parce qu'un nom peut changer et ne garantit pas l'unicité.
