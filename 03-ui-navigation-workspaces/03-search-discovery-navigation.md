# 03 — Search, Navigation & Discovery

## 1. Search before create

La règle la plus importante de saisie dans HOPEX :

```text
SEARCH
→ VERIFY
→ REUSE
→ CREATE only if needed
```

La recherche est donc un mécanisme de **qualité du repository**, pas seulement un confort UX.

## 2. Rechercher avec plusieurs clés

Un objet peut être connu sous plusieurs noms :

```text
Payment Orchestrator
Payment Hub
PayOrch
APP-0042
```

Avant création, chercher :

- nom officiel ;
- ancien nom ;
- acronyme ;
- identifiant externe ;
- owner ;
- domaine ;
- technologie associée si nécessaire.

## 3. Recherche exacte vs exploration

Deux besoins différents :

### Je connais l'objet

```text
External ID / canonical name
→ object
```

### Je découvre un domaine

```text
Payment domain
→ filtered list
→ classification
→ relationships
→ candidate objects
```

## 4. Navigation par relations

Une fois l'objet trouvé, éviter de revenir systématiquement au moteur de recherche.

Exemple :

```text
Payment Orchestrator
→ supported Business Processes
→ supporting Technologies
→ connected Applications
→ Owners
→ Initiatives
```

Cette navigation permet de suivre le graphe réel du repository.

## 5. Navigation top-down

Pour comprendre un domaine :

```text
Business Goal
→ Capability
→ Process
→ Application
→ Technology
→ Infrastructure / source externe
```

## 6. Navigation bottom-up

Pour une analyse d'impact :

```text
Technology
→ Applications using it
→ Processes supported
→ Capabilities/business outcomes affected
```

## 7. Recherche de doublons

Avant création d'une Application :

```text
same external ID?
same canonical name?
same owner + same domain?
same old name?
same relationships?
```

Un résultat ressemblant à 80 % doit déclencher une vérification humaine, pas une création automatique.

## 8. MayaBank — scénario

Demande : "Cartographier Kafka".

Ne pas commencer par créer `Kafka`.

Faire :

```text
Search Kafka
→ Search Event Streaming
→ inspect existing Software Technology / Platform objects
→ inspect applications already related
→ inspect standards/catalog entries
→ decide whether an existing canonical object covers the need
```

## 9. Search vs classification

La recherche textuelle ne remplace pas la classification.

Un bon repository doit permettre :

```text
Find all strategic payment applications
```

sans dépendre du mot `payment` dans leur nom.

Il faut donc des propriétés/relations gouvernées :

```text
Domain = Payments
Lifecycle = Strategic
Criticality = Critical
```

## 10. Recherche orientée question

Mauvais :

```text
Je cherche "OpenShift".
```

Meilleur :

```text
Je veux connaître toutes les applications critiques qui dépendent de la plateforme OpenShift et dont la fin de support technologique tombe avant leur date de remplacement.
```

La deuxième formulation indique les objets, relations et propriétés à exploiter.

## 11. Anti-patterns

- créer dès que la recherche exacte échoue ;
- rechercher uniquement par nom ;
- utiliser des acronymes non documentés ;
- dupliquer un objet entre deux domaines ;
- maintenir une liste Excel parallèle pour retrouver les objets ;
- naviguer uniquement par arborescence et ignorer les relations.

## 12. Lab

Pour chacun des objets suivants :

```text
Payment Orchestrator
Fraud Engine
Kafka / Event Streaming
OpenShift
Instant Payment Process
```

produire :

1. clés de recherche ;
2. MetaClass attendue ;
3. relations permettant de confirmer l'identité ;
4. règle de décision REUSE/CREATE ;
5. risque de doublon principal.