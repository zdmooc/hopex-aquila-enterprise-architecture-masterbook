# 07 — Data Classification, Privacy, Security & Retention

## 1. Classification

La classification traduit le niveau de sensibilité et les exigences de traitement.

Taxonomie pédagogique MayaBank :

```text
Public
Internal
Confidential
Restricted
```

Le client doit utiliser sa taxonomie réelle.

## 2. Exemples

| Information | Classification pédagogique |
|---|---|
| Public product description | Public |
| Internal architecture metadata | Internal |
| Customer contact | Confidential |
| Authentication secret | Restricted |
| Payment credential / sensitive identifier | Restricted selon politique |

## 3. Classification inheritance

La classification peut se propager à :

```text
Information concept
→ logical attributes
→ API/event contract
→ data store
→ export/report
```

Mais l’héritage doit être gouverné : une agrégation anonymisée peut avoir une classification différente.

## 4. Personal Data

L’architecture doit identifier :

- catégories de personnes ;
- catégories de données ;
- finalités ;
- applications/processes ;
- storage locations ;
- recipients ;
- retention ;
- controls.

## 5. Privacy by design

Questions :

```text
Do we need the data?
For which purpose?
How long?
Who can access it?
Can it be minimized?
Can it be pseudonymized?
Where does it flow?
How is deletion propagated?
```

## 6. Data minimization

Un event ou API ne doit pas embarquer toute l’entité client « au cas où ».

Exemple :

```text
PaymentStatusChanged
```

n’a pas besoin d’inclure automatiquement adresse, téléphone et identité complète du client.

## 7. Encryption

Architecture-level controls :

- encryption in transit ;
- encryption at rest ;
- key management ;
- secret management ;
- field-level protection lorsque nécessaire.

Les mécanismes techniques seront approfondis Partie X.

## 8. Access control

Modèles possibles :

- RBAC ;
- ABAC ;
- purpose-based restrictions ;
- row/column-level security ;
- privileged access.

Le repository doit documenter les exigences structurantes sans devenir un annuaire IAM opérationnel.

## 9. Segregation of duties

Exemple :

```text
Developer
≠ production data administrator

Fraud analyst
≠ payment approver automatically
```

Les responsabilités doivent être alignées avec risques et contrôles.

## 10. Masking and tokenization

Utiles notamment pour :

- non-production environments ;
- analytics ;
- support ;
- data sharing.

Documenter si la transformation est réversible, le niveau de risque et les usages permis.

## 11. Retention

Une retention rule contient :

```text
Data category
Trigger
Retention duration
Legal/business basis
Archive rule
Deletion rule
Owner
Exceptions/legal hold
```

Ne pas inventer de durée réglementaire dans le masterbook.

## 12. Deletion propagation

Dans un SI distribué :

```text
Source deletion
→ replicas
→ caches
→ search indexes
→ analytics
→ backups according to policy
→ downstream processors
```

La suppression est une architecture, pas un simple `DELETE` SQL.

## 13. Backup vs retention

Backup = mécanisme de résilience.

Retention = durée de conservation gouvernée.

Un backup ne doit pas devenir une excuse pour conserver indéfiniment sans politique.

## 14. Data residency

Pour les architectures multi-cloud/multi-region :

- location ;
- replication region ;
- legal constraints ;
- cross-border transfer ;
- DR site.

Documenter la contrainte au niveau information/data store/deployment.

## 15. MayaBank Privacy Map

```text
Customer Identity
→ Customer Master
→ IAM / Fraud / Payments as authorized consumers
→ classification: sensitive
→ retention governed
→ lineage documented
```

## 16. Security impact analysis

Question : ajout d’un nouveau consumer analytics.

```text
Dataset
→ classification
→ personal/sensitive elements
→ lawful business use
→ access model
→ masking
→ retention
→ export controls
```

## 17. Non-production data

Anti-pattern majeur : copie brute de production en dev/test.

Target :

```text
synthetic data
or
masked/tokenized subset
with governed exception process
```

## 18. Data sharing

Avant partage interne/externe :

1. purpose ;
2. owner approval ;
3. contract ;
4. minimal dataset ;
5. classification ;
6. access ;
7. retention ;
8. monitoring ;
9. termination process.

## 19. Compliance linkage

Les pages publiques HOPEX Data Governance positionnent la solution sur data compliance, privacy et connexion aux risques/contrôles.

Le repository peut relier :

```text
Data
→ Regulation/Requirement
→ Risk
→ Control
→ Process/Application
```

## 20. Anti-patterns

- classification uniquement au niveau base ;
- `Confidential` partout donc inutilisable ;
- retention sans trigger ;
- backup = archive ;
- PII copiée dans chaque event ;
- production data dans dev sans contrôle ;
- suppression sans analyse downstream ;
- access list statique dans un diagramme EA.
