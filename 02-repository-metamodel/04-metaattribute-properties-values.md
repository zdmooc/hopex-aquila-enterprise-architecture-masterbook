# 04 — MetaAttribute, Properties & Values

## 1. Une propriété doit servir une décision

Ajouter des champs n'améliore pas automatiquement le repository.

Un attribut utile répond à une question d'architecture ou de gouvernance.

Exemples :

```text
Owner
Lifecycle
Criticality
Business fit
Technical fit
Review date
External source
```

## 2. MetaAttribute

Le métamodèle HOPEX expose le concept `MetaAttribute` dans son API MetaModel publique.

Mental model :

```text
MetaClass Application
  ├─ MetaAttribute Name
  ├─ MetaAttribute Lifecycle
  ├─ MetaAttribute Criticality
  └─ MetaAttribute Vendor
```

Puis :

```text
Object Payment Orchestrator
  Name        = "MayaBank Payment Orchestrator"
  Lifecycle   = "Strategic"
  Criticality = "Critical"
```

Les noms exacts des attributs disponibles doivent être vérifiés sur la configuration HOPEX réelle.

## 3. Valeur libre vs valeur contrôlée

### Libre

```text
Description = texte
Comment = texte
```

### Contrôlée

```text
Lifecycle ∈ {Emerging, Strategic, Tolerate, Retire}
```

Pour le reporting, les valeurs contrôlées sont généralement préférables lorsque le domaine est fini.

## 4. Pourquoi les listes contrôlées comptent

Sans gouvernance :

```text
Retire
To Retire
Retired
Obsolete
Decommission
To be decommissioned
```

Un tableau de bord devient faux ou complexe.

Avec référentiel de valeurs :

```text
Lifecycle = Retire
```

et les nuances sont portées par d'autres propriétés si nécessaire.

## 5. Valeur absente ≠ valeur négative

```text
Criticality = null
```

ne signifie pas :

```text
Criticality = Low
```

Les rapports doivent distinguer :

- inconnu ;
- non applicable ;
- faible ;
- non évalué.

## 6. Propriétés calculées et dérivées

Certaines informations peuvent être calculées à partir d'autres données plutôt que saisies manuellement.

Exemple conceptuel :

```text
Application Risk Score
= f(criticality, obsolescence, incidents, dependency risk)
```

Éviter de saisir à la main une donnée calculable si cela crée une divergence.

## 7. Propriétés externes

Une propriété synchronisée doit avoir :

- une source ;
- une fréquence ;
- une règle de conflit ;
- un owner de la donnée ;
- une politique si la source devient indisponible.

Exemple :

```text
Runtime Version
Source = ServiceNow CMDB
Mode   = inbound only
```

## 8. Propriétés d'architecture vs inventaire

Ne pas importer tous les champs d'une source externe.

Question :

```text
Ce champ permet-il une analyse, une décision ou une gouvernance ?
```

Sinon, il peut rester dans la source opérationnelle.

## 9. Règles de qualité

Pour chaque attribut important :

| Question | Exemple |
|---|---|
| définition | que signifie Criticality ? |
| type | liste, texte, date, nombre |
| valeurs | domaine autorisé |
| obligatoire ? | oui/non/conditionnel |
| owner | qui tranche ? |
| source | HOPEX, CMDB, finance... |
| fréquence | mensuelle, événementielle... |
| usage | rapport, roadmap, filtre... |

## 10. MayaBank — fiche minimale Application

```text
Name
Description
Owner
Domain
Lifecycle
Criticality
Business fit
Technical fit
Review date
Source system
External key
```

Ce n'est pas une déclaration du schéma standard HOPEX ; c'est un **modèle de gouvernance pédagogique** à mapper sur les attributs réellement disponibles.

## 11. MayaBank — Technology

```text
Name
Vendor
Product family
Version policy
Lifecycle
Strategic status
End-of-support date
Owner
Approved / Restricted / Retire
```

## 12. Anti-patterns

- champ libre pour une valeur qui devrait être contrôlée ;
- 80 propriétés obligatoires à la création ;
- attribut jamais utilisé dans aucun rapport ;
- même information stockée dans trois propriétés ;
- propriété calculée maintenue manuellement ;
- valeur par défaut utilisée pour masquer `unknown` ;
- import qui écrase des données gouvernées localement.

## 13. Questions d'entretien

**Comment choisissez-vous les propriétés d'une Application ?**  
À partir des décisions et analyses attendues, puis en définissant type, source, owner, fréquence et règles de qualité.

**Pourquoi limiter les attributs ?**  
Parce que chaque attribut crée un coût de collecte, de qualité et de gouvernance.
