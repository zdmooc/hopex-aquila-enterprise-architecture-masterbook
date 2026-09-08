# 11 — Governance & Anti-patterns

## 1. Le métamodèle est un actif gouverné

Modifier le métamodèle change la manière dont l'entreprise est représentée. Cette décision doit donc être traitée comme une décision d'architecture, pas comme une simple personnalisation d'écran.

## 2. Gouvernance proposée

```text
Need identified
→ semantic analysis
→ standard model check
→ impact assessment
→ design proposal
→ review board
→ sandbox implementation
→ regression tests
→ deployment package
→ production rollout
→ post-release validation
```

## 3. Rôles

### Metamodel Owner
Décide de la cohérence globale du modèle.

### Domain Architect
Porte le besoin métier/architecture.

### HOPEX Administrator / Configurator
Implémente et teste la configuration.

### Integration Architect
Vérifie APIs, imports et synchronisations.

### Data Steward
Vérifie la qualité des objets et propriétés.

### Architecture Board
Arbitre les extensions structurantes.

## 4. Registre de customisation

Pour chaque extension :

```text
ID
Name
Type: attribute / association / metaclass / list
Business rationale
Owner
Introduced version
Affected solutions
Affected schemas/APIs
Affected reports
Migration notes
Status
```

## 5. Anti-pattern — MetaClass par produit

```text
MetaClass Kafka
MetaClass OpenShift
MetaClass Oracle
MetaClass Azure
```

Problème : on confond **produit** et **nature architecturale**.

Solution : utiliser une MetaClass technologique générique appropriée et des instances.

## 6. Anti-pattern — copier un Excel

```text
Excel column → MetaAttribute
Excel tab → MetaClass
```

sans analyse sémantique.

Le tableur reflète souvent un format historique, pas un modèle conceptuel.

## 7. Anti-pattern — relation universelle

```text
Association
Association
Association
```

partout.

Le repository devient connecté mais non sémantique.

## 8. Anti-pattern — tout obligatoire

Rendre 40 champs obligatoires :

- ralentit la création ;
- produit de fausses valeurs ;
- décourage les contributeurs ;
- masque les données réellement critiques.

Définir un **minimum viable record**.

## 9. Anti-pattern — statut fourre-tout

```text
Status = Strategic
Status = Prod
Status = Validated
Status = Retire
```

Ces valeurs parlent de dimensions différentes.

Séparer :

```text
Lifecycle
Validation state
Environment
Strategic disposition
```

## 10. Anti-pattern — import autoritaire

Une source externe écrase :

- owner ;
- lifecycle ;
- classification ;
- commentaires d'architecture.

Solution : définir la maîtrise **champ par champ**.

## 11. Anti-pattern — extension sans tests API

Une customisation fonctionne dans l'UI mais casse :

```text
GraphQL schema
REST consumer
import template
report
integration ServiceNow
```

Les tests de régression doivent couvrir plusieurs surfaces.

## 12. Anti-pattern — doublon de classe standard

Exemple :

```text
Standard Application
Custom Business Application
Custom IT Application
```

sans différence stable.

Résultat : analyses fragmentées et migrations coûteuses.

## 13. Anti-pattern — objets orphelins

Un repository rempli d'objets sans relations :

```text
inventory ≠ architecture knowledge
```

Objectif : relier seulement les concepts nécessaires mais suffisamment pour répondre aux concerns.

## 14. Anti-pattern — cycles hiérarchiques

```text
Capability A parent B
Capability B parent C
Capability C parent A
```

Les hiérarchies doivent être acycliques.

## 15. Anti-pattern — personnalisation locale invisible

Une équipe crée une extension sans informer :

- les autres domaines ;
- l'équipe API ;
- l'équipe upgrade ;
- la gouvernance.

Résultat : dépendance cachée.

## 16. Definition of Done d'une extension

Une extension n'est terminée que si :

- définition approuvée ;
- owner identifié ;
- MetaClass/attribute/association documenté ;
- UI testée ;
- permissions testées ;
- import/export testés si concernés ;
- GraphQL/REST testés si concernés ;
- rapports testés ;
- upgrade notes documentées ;
- exemple MayaBank ou client validé.

## 17. Review trimestrielle

Questions :

1. quelles customisations sont encore utilisées ?
2. le standard HOPEX couvre-t-il maintenant un besoin custom ?
3. quelles extensions n'ont plus d'owner ?
4. quelles propriétés ne sont jamais renseignées ?
5. quelles valeurs de liste ne sont jamais utilisées ?
6. quels objets sont devenus orphelins ?
7. quelles APIs dépendent d'un mapping custom ?

## 18. Matrice de risque

| Changement | Risque |
|---|---|
| nouveau libellé | faible |
| nouvelle valeur de liste | faible/moyen |
| nouvel attribut | moyen |
| nouvelle association | moyen/fort |
| nouvelle MetaClass | fort |
| modification structurante d'une classe standard | très fort |

## 19. MayaBank — décision type

Demande : « ajouter un type d'application `PaymentCriticalApplication` ».

Analyse :

```text
Nature différente ? non
Besoin = classification de criticité paiement
Solution = attribut/classification si possible
MetaClass custom = rejetée
```

## 20. Questions d'entretien

**Qui doit posséder le métamodèle ?**  
Une gouvernance transverse, pas une seule équipe projet.

**Quel est le risque d'une forte customisation ?**  
Coût d'upgrade, fragmentation sémantique, dépendances API et difficulté de support.
