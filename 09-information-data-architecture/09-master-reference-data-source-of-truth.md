# 09 — Master Data, Reference Data & Source of Truth

## 1. Pourquoi le sujet est critique

Les transformations échouent souvent parce que plusieurs systèmes revendiquent la même autorité.

Question centrale :

```text
For this information,
which system/process is authoritative,
and under which conditions?
```

## 2. Source of Truth vs System of Record

Dans le masterbook :

### System of Record
Système officiellement responsable d’un enregistrement ou domaine selon une règle de gouvernance.

### Source of Truth
Source considérée comme autoritative pour un usage ou une information donnée.

Les termes sont souvent utilisés différemment selon les organisations ; il faut définir la convention client.

## 3. Master Data

Exemples :

- Customer ;
- Product ;
- Legal Entity ;
- Counterparty.

Caractéristiques :

- partagée ;
- durable ;
- réutilisée ;
- identité importante ;
- qualité critique.

## 4. Reference Data

Exemples :

```text
Currency
Country
Payment Scheme
Reason Code
Status Code
```

La gouvernance doit préciser :

- authoritative source ;
- update frequency ;
- distribution ;
- version/effective date ;
- consumers.

## 5. Identity resolution

Pour Customer :

```text
CustomerNumber
PartyId
CRMId
IAMSubjectId
ExternalSchemeId
```

Ne pas considérer ces identifiants comme identiques sans mapping gouverné.

## 6. Golden record process

Un golden record peut nécessiter :

```text
Match
→ merge
→ survivorship rules
→ stewardship review
→ publish
```

Le résultat doit avoir ownership et lineage.

## 7. Data duplication

Toute duplication n’est pas mauvaise.

### Duplication légitime

- cache ;
- read model ;
- analytics copy ;
- DR replica ;
- immutable event history.

### Duplication risquée

- deux masters concurrents ;
- synchronisation manuelle ;
- copies sans ownership ;
- fields divergents sans reconciliation.

## 8. Authoritative matrix MayaBank

| Information | Authoritative source | Derived copies |
|---|---|---|
| Customer profile | Customer Master | Fraud context, channel cache |
| Account balance | Core Account | payment read model |
| Payment state | Payment Orchestrator/Payment Store | events, analytics |
| Fraud decision | Fraud Decision Service | audit/reporting copy |
| Currency codes | Reference Data Service | caches |

Pédagogique : à adapter au SI réel.

## 9. Ownership conflict

Scénario : CRM et Core portent tous deux l’adresse client.

Questions :

1. définition identique ?
2. même finalité ?
3. quelle source est autoritative ?
4. qui peut modifier ?
5. comment propager ?
6. quelle latence acceptable ?
7. quelle reconciliation ?

## 10. Reference data distribution

Patterns :

- central API ;
- replicated cache ;
- event publication ;
- scheduled file ;
- embedded code list.

Éviter les listes codées en dur dispersées sans versioning.

## 11. Effective dating

Certaines références ont :

```text
Valid From
Valid To
Version
Status
```

Important pour reconstituer une décision passée.

## 12. Reconciliation

Pour des copies dérivées :

```text
Source
→ expected replica
→ compare
→ discrepancy
→ repair/escalate
```

## 13. Conflict resolution

En distribution bidirectionnelle, définir :

- ownership by attribute ;
- timestamps/version ;
- business priority ;
- manual stewardship ;
- deterministic merge rules.

## 14. Master data and bounded contexts

Un MDM global ne signifie pas qu’un seul modèle sert tous les contextes.

```text
Golden Customer
→ shared identity

Fraud Customer View
→ context-specific projection
```

## 15. Source-of-truth change

Migrer la source autoritative nécessite :

1. data profiling ;
2. mapping ;
3. migration ;
4. dual-run éventuel ;
5. reconciliation ;
6. consumer cutover ;
7. old source freeze ;
8. decommission.

## 16. Data authority lineage

Le repository doit permettre :

```text
Information
→ authoritative application/store
→ producers
→ consumers
→ copies
→ transformation
```

## 17. Anti-patterns

- « database = truth » sans gouvernance ;
- plusieurs masters silencieux ;
- golden record sans owner ;
- reference data codée partout ;
- copie analytique utilisée pour transaction ;
- aucune reconciliation ;
- changement de master sans consumer impact analysis.
