# 02 — Taxonomy, L0/L1/L2/L3 et décomposition

## 1. Pourquoi une taxonomie

Une carte de capacités devient exploitable quand ses niveaux ont une règle stable.

```text
L0 = domaine d'entreprise
L1 = grande capability
L2 = sous-capability significative
L3 = niveau détaillé utilisé seulement s'il sert une analyse ou une décision
```

Le nombre de niveaux n'est pas une vérité universelle. MayaBank utilise L0 à L3 comme convention pédagogique.

## 2. Exemple MayaBank

```text
L0 Payments
 ├─ L1 Payment Initiation
 │   ├─ L2 Instant Payment Initiation
 │   └─ L2 Scheduled Payment Initiation
 ├─ L1 Payment Processing
 │   ├─ L2 Payment Validation
 │   ├─ L2 Payment Routing
 │   └─ L2 Payment Settlement Coordination
 └─ L1 Payment Operations
     ├─ L2 Exception Handling
     └─ L2 Reconciliation
```

## 3. Règles de nommage

Préférer une formulation orientée aptitude :

- `Payment Routing`
- `Customer Identity Management`
- `Fraud Decisioning`
- `Data Quality Management`

Éviter :

- noms d'équipe ;
- noms de produits ;
- verbes très opérationnels ;
- phrases de projet.

## 4. Critères de décomposition

Décomposer seulement si au moins un des critères suivants est vrai :

- ownership différent ;
- maturité différente ;
- importance stratégique différente ;
- investissements différents ;
- applications de support différentes ;
- roadmap différente ;
- risque différent.

## 5. Anti-pattern : taxonomie organisationnelle

```text
Payments Department
→ Fraud Team
→ Platform Team
```

Ce n'est pas une capability map ; c'est un organigramme déguisé.

## 6. Anti-pattern : micro-capabilities

```text
Validate IBAN
Parse ISO20022
Write Audit Log
```

Ces détails peuvent appartenir à des processus, règles, services ou composants, mais deviennent souvent trop fins pour une carte stratégique.

## 7. Anti-pattern : trous de niveau

Une L3 ne devrait pas être créée simplement parce qu'un sujet technique est important. La hiérarchie doit rester sémantiquement cohérente.

## 8. Capability decomposition review

Pour chaque capability enfant, poser :

1. est-elle réellement une partie de la capability parent ?
2. possède-t-elle une définition non ambiguë ?
3. peut-on l'évaluer indépendamment ?
4. peut-on lui associer un owner ?
5. sert-elle une décision ?

## 9. Repository rules

Dans HOPEX, la hiérarchie doit être gouvernée comme des données :

- parent canonique ;
- enfants canoniques ;
- pas de doublon local dans un diagramme ;
- conventions de nommage ;
- owner/steward ;
- historique des changements significatifs.

## 10. Cartes par audience

Une même taxonomie peut être projetée différemment :

- Executive : L0/L1 ;
- Business Architect : L1/L2 ;
- Domain Architect : L2/L3 ;
- Investment Board : capabilities avec heatmap et initiatives.

La vue change, pas les objets canoniques.