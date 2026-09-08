# 06 — Personas, Workspaces et responsabilités

## 1. HOPEX est multi-personas

Le Web Front-End HOPEX Aquila est destiné à plusieurs profils. Cela implique que le même repository doit proposer des expériences adaptées aux responsabilités de chacun.

Un bon design de gouvernance ne donne pas simplement « accès à HOPEX ». Il définit :

```text
Persona
→ objectives
→ objects needed
→ actions allowed
→ views/reports
→ validation responsibilities
```

## 2. Enterprise Architect

Responsabilités typiques :

- cohérence du métamodèle ;
- cartographie cross-domain ;
- principes et standards ;
- dépendances ;
- architecture cible ;
- roadmaps ;
- gouvernance du repository.

MayaBank : relier paiements, capabilities, applications, data, technology et transformation.

## 3. Solution Architect

Préoccupations :

- périmètre projet ;
- interfaces ;
- dépendances ;
- technologies ;
- NFR ;
- conformité aux standards ;
- impacts sur l'existant.

HOPEX ne remplace pas les dossiers détaillés de conception, mais peut maintenir les objets et décisions structurantes partagées avec l'entreprise.

## 4. Business Architect

Préoccupations :

- capabilities ;
- value delivery ;
- organisations ;
- processes ;
- services métier ;
- transformation métier.

MayaBank : Real-Time Payment Processing, Fraud Management, Customer Notification, Settlement & Reconciliation.

## 5. Application Portfolio Manager

Préoccupations :

- inventaire applicatif ;
- owner ;
- lifecycle ;
- coûts/risques selon données disponibles ;
- rationalisation ;
- roadmap ;
- obsolescence.

## 6. Process Modeler / Process Owner

Préoccupations :

- processus ;
- acteurs ;
- responsabilités ;
- inputs/outputs ;
- applications support ;
- risques/contrôles selon périmètre.

## 7. Data / Information Architect

Préoccupations :

- information concepts ;
- ownership ;
- sources ;
- flux ;
- systèmes de référence ;
- classification ;
- lineage au niveau pertinent.

## 8. Risk Manager / Auditor

Le front HOPEX vise aussi des profils GRC. Le repository partagé permet de relier les risques et contrôles aux processus, applications ou technologies quand les solutions concernées sont en place.

## 9. Repository Steward

Rôle critique souvent oublié.

Responsabilités :

- qualité ;
- doublons ;
- complétude ;
- taxonomie ;
- processus de revue ;
- coordination des owners ;
- contrôle des imports.

Le steward ne doit pas devenir le propriétaire métier de toutes les données.

## 10. Platform Administrator

Préoccupations :

- utilisateurs ;
- droits ;
- configuration ;
- environnements ;
- modules ;
- upgrades ;
- monitoring ;
- sauvegardes ;
- sécurité ;
- intégrations techniques.

## 11. Developer / Integration Engineer

Préoccupations :

- GraphQL ;
- REST ;
- authentication ;
- mappings ;
- pagination ;
- mutations ;
- erreurs ;
- logs ;
- ServiceNow ;
- MCP.

## 12. Executive / Decision Maker

Le dirigeant ne doit pas parcourir le métamodèle complet.

Il attend :

```text
Decision
→ evidence
→ concise view
→ KPI / risk / roadmap
```

Exemple CIO MayaBank :

- quelles applications paiement doivent être retirées ?
- quelles dépendances bloquent la cible ?
- quelles technologies sont obsolètes ?
- quelles initiatives ferment quels gaps ?

## 13. RACI de gouvernance simplifié

| Activité | EA | Owner | Steward | Admin |
|---|---|---|---|---|
| définir métamodèle opérationnel | A/R | C | C | C |
| valider contenu métier | C | A/R | C | - |
| contrôler qualité | C | C | A/R | - |
| gérer droits/modules | C | - | C | A/R |
| définir intégration | A | C | C | R |
| arbitrer lifecycle | C | A/R | C | - |

C'est une matrice pédagogique à adapter.

## 14. Principle of least privilege

Le droit de consulter, modifier, approuver ou administrer doit être adapté au besoin.

Ne pas confondre :

```text
can see
can edit
can validate
can administer
can integrate
```

Ces capacités n'ont pas la même portée.

## 15. Workflow de revue recommandé

```text
Contributor updates object
→ owner reviews meaning
→ steward checks repository quality
→ architecture authority checks consistency if required
→ object becomes trusted/published
```

La mécanique exacte de workflow HOPEX sera étudiée lorsque la documentation et l'environnement concernés seront disponibles.

## 16. Cas MayaBank

`Payment Orchestrator` :

- Business owner : Head of Payments ;
- IT owner : Payment Platform Manager ;
- Architect : Payments Solution Architect ;
- Steward : EA Repository Steward ;
- source technique : architecture team ;
- runtime evidence : ServiceNow/Discovery selon intégration.

Cette séparation réduit le risque de données « sans propriétaire ».
