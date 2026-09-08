# 13 — Official & Public Sources for IT Architecture

## 1. Règle de preuve

Cette partie distingue trois niveaux :

```text
A — source produit actuelle
B — source publique historique HOPEX
C — pratique pédagogique / recommandation d'architecture
```

Un comportement observé dans une ancienne release ne doit pas être présenté comme preuve d'un écran Aquila 6.2 actuel.

## 2. Source actuelle — Enterprise Architecture Tool

Bizzdesign/MEGA présente HOPEX comme une plateforme EA connectant notamment :

- applications ;
- processus ;
- business capabilities ;
- data flows ;
- application interdependencies ;
- technology investments ;
- technology lifecycle ;
- business impact analysis ;
- application rationalization ;
- cloud migration.

URL :

https://siteprod.mega.com/enterprise-architecture-ea-tool

Usage dans ce masterbook : **source A** pour les use cases globaux.

## 3. Source actuelle — HOPEX Aquila 6.2.18 bundle

Le Store publie un bundle HOPEX Aquila 6.2.18 et rappelle les axes :

- Connected EA ;
- automation / discovery ;
- auto-diagramming ;
- dashboards / insights ;
- application rationalization ;
- cloud migration.

URL :

https://store.mega.com/Bundles/details/817aa44c-d7ed-47cb-b962-f9d303861a8c

Usage : **source A** pour la baseline Aquila et le positionnement produit.

## 4. Source actuelle — Core Back-End

HOPEX Core Back-End Aquila 6.2 :

https://store.mega.com/modules/details/hopex.core

Le Core est présenté comme la couche de logique métier et d'accès au repository, connectant business, IT, data et risk dans une plateforme commune.

Usage : **source A**.

## 5. Source actuelle — Web Front-End

HOPEX Web Front-End :

https://store.mega.com/modules/details/hopex.dtpx

La fiche liste HOPEX IT Architecture parmi les key features/solutions accessibles au travers du Web Front-End.

Usage : **source A** pour confirmer l'existence de HOPEX IT Architecture dans l'écosystème Aquila.

## 6. Source publique historique — Application Scenario Diagrams

Community article :

https://community.mega.com/t5/Image-Gallery/Application-Scenario-Diagrams/td-p/15543

La ressource explique que des scenario diagrams permettent aux application architects de représenter la même application dans plusieurs contextes et de décrire les flows entre applications, avec possibilité de regrouper des interactions.

Usage : **source B**.

Ne pas en déduire que le même écran, nom de menu ou workflow existe inchangé dans Aquila 6.2.

## 7. Source publique historique — Application Environment auto-diagram

Community How-To :

https://community.mega.com/t5/Hopex-How-To-Videos/How-to-automatically-create-an-Application-Environment-diagram/td-p/31353

La ressource montre la génération automatique d'un Application Environment diagram à partir de flows.

Usage : **source B** pour le concept d'environnement applicatif et d'auto-diagramming.

## 8. Source publique historique — Deployment Environment

HOPEX V5 Release Notes CP5 :

https://community.mega.com/mega/attachments/mega/support-blog/156/2/HOPEX_V5_Release%20Note%20CP5.pdf

La section HOPEX IT Architecture documente un `Application System Deployment Environment` pour définir le contexte d'intégration et les dépendances d'un déploiement, y compris un shared data server.

Usage : **source B** pour le concept de deployment context.

## 9. Ce qui est factuel dans la Partie IV

Peut être présenté comme factuel au niveau produit :

- HOPEX propose un use case Enterprise Architecture connecté ;
- HOPEX IT Architecture fait partie de l'écosystème Web Front-End ;
- l'offre met en avant applications, capabilities, process, flows et technologies ;
- le positionnement actuel inclut automatic discovery/mapping et impact analysis ;
- l'offre met en avant technology lifecycle, rationalization et cloud migration.

## 10. Ce qui est pédagogique

Les éléments suivants sont des patterns du masterbook, sauf validation dans une instance client :

- valeurs exactes `Strategic / Mainstream / Retire` ;
- noms exacts des MetaClasses ;
- noms exacts des propriétés ;
- RACI MayaBank ;
- architecture cible MayaBank ;
- milestones et dates ;
- taxonomie de standards ;
- score de technical health ;
- structure des quality gates.

## 11. Ce qui doit être vérifié en mission

Avant d'utiliser le contenu comme procédure opérationnelle :

1. version Core exacte ;
2. Web Front-End exact ;
3. licences ;
4. solutions installées ;
5. metamodel standard/custom ;
6. MetaClasses disponibles ;
7. property pages ;
8. workflows ;
9. diagram types ;
10. lifecycle classifiers ;
11. integrations ;
12. data sources.

## 12. Source de vérité vs exemple

Le cas MayaBank ne doit jamais être pris pour une configuration HOPEX standard.

```text
HOPEX product facts
→ sources officielles/publics MEGA/Bizzdesign

MayaBank model
→ architecture pédagogique
```

## 13. Copyright

Le dépôt :

- ne redistribue pas de documentation propriétaire ;
- ne reproduit pas de captures propriétaires ;
- ne contient pas de backup HOPEX ;
- ne copie pas de training material ;
- fournit des explications originales et liens vers les sources publiques.

## 14. Revalidation

Les sources produit seront revérifiées dans la Partie XXIV au moment de l'audit final, car les builds Aquila évoluent régulièrement.
