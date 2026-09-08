# 99 — Sources officielles, faits vérifiés et frontière pédagogique

## 1. Règle de cette partie

Trois niveaux restent séparés :

```text
Fait produit vérifié
≠ recommandation d’architecture
≠ hypothèse pédagogique MayaBank
```

Les URLs ci-dessous sont des références publiques consultées en septembre 2026.

# 2. Bizzdesign Hopex — plateforme

## Bizzdesign Hopex

https://bizzdesign.com/transformation-suite/hopex

La page publique positionne Hopex comme une plateforme connectée couvrant notamment :

- Enterprise Architecture Management ;
- Application Portfolio Management ;
- Technology Portfolio Management ;
- Business Process Management ;
- Data Management ;
- Governance, Risk and Compliance ;
- repository connecté ;
- intégrations avec des outils tiers ;
- reports/dashboards/enterprise portal.

Ce masterbook utilise ces capacités comme contexte produit général.

# 3. HOPEX Core Back-End Aquila 6.2

https://store.mega.com/modules/details/hopex.core

Baseline vérifiée :

```text
HOPEX Core Back-End Aquila 6.2
branch: 62.18.x
latest observed build: 62.18.0+774
published: 2026-09-03
```

La page Store décrit le Core comme le back-end portant la logique et l’accès au repository, avec connexion des perspectives business, IT, data et risk.

# 4. IT-Pedia connector

https://store.mega.com/modules/details/itpm.itpedia

Faits publics vérifiés :

- intégration avec Eracent IT-Pedia ;
- import de nouvelles technologies ;
- alignement avec les technologies existantes du repository ;
- mise à jour des technologies importées ;
- comparaison avant/après ;
- analyse de l’impact sur les indicateurs d’obsolescence ;
- utilisation avec les solutions HOPEX IT Portfolio Management / IT Business Management Aquila selon prérequis/licence.

Version publique observée en septembre 2026 :

```text
62.7.0+7206
published 2026-03-17
```

Le connector fournit des données et workflows d’intégration ; il ne décide pas à la place de l’entreprise de ses standards internes.

# 5. ITPM Excel Import Template

https://store.mega.com/modules/details/itpm.importexceltemplate

La ressource publique montre l’existence d’un template d’import ITPM Aquila et d’un onglet / contenu autour des Software Technologies, notamment un champ Vendor dans les évolutions documentées.

Le masterbook ne reproduit pas le template sous licence.

# 6. Support Bizzdesign Hopex

https://help.bizzdesign.com/

Le portail public distingue documentation, releases, support et training pour Hopex.

Pour une mission réelle, les écrans et propriétés exacts doivent être vérifiés dans la documentation associée au tenant/version/licence du client.

# 7. Bizzdesign Hopex SLA

Référence publique :

https://bizzdesign.com/sites/default/files/2026-01/Bizzdesign%20Hopex%20Service%20Level%20Agreement%20v20260123%20EN.pdf

Ce document décrit l’offre SaaS Hopex et certains niveaux d’architecture/sécurité du service Hopex lui-même.

Il ne doit pas être confondu avec la Technology Architecture des systèmes que l’utilisateur modélise dans HOPEX.

# 8. OpenShift — documentation officielle Red Hat

## Control plane architecture

https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/architecture/control-plane

La documentation publique explique notamment :

- control plane machines ;
- worker/compute machines ;
- machine config pools ;
- operators ;
- etcd ;
- scheduling des workloads sur les workers.

Ces éléments supportent les explications conceptuelles du chapitre OpenShift.

Le masterbook ne prétend pas décrire une topologie OpenShift universelle : le design réel dépend de version, plateforme, installation et exigences.

# 9. Kubernetes — documentation officielle

https://kubernetes.io/docs/concepts/architecture/

Référence générale pour control plane, nodes, pods, scheduling et composants de cluster.

Dans le masterbook, Kubernetes/OpenShift sont utilisés comme technologies et plateformes de référence ; ils ne constituent pas des fonctionnalités HOPEX.

# 10. Sources à utiliser en mission pour le lifecycle

Pour tout produit technologique :

1. documentation officielle vendor ;
2. lifecycle/support policy officielle ;
3. bulletin sécurité officiel ;
4. contrats/support client ;
5. IT-Pedia si intégré ;
6. standard interne Architecture Board.

Ne pas définir une date EOL à partir d’un blog ou d’une mémoire non vérifiée.

# 11. Faits produit retenus

On peut affirmer dans cette Partie X :

- Hopex relie des perspectives business/IT/data/risk dans une plateforme commune ;
- Bizzdesign Hopex expose une solution Technology Portfolio Management ;
- un connecteur IT-Pedia officiel existe pour enrichir et actualiser des technologies et leurs informations de cycle de vie ;
- HOPEX Core Aquila 6.2 branche 62.18.x est la baseline actuelle du masterbook ;
- le détail du métamodèle, des vues, workflows, droits et licences doit être validé dans l’environnement client.

# 12. Recommandations du masterbook

Ne sont pas présentées comme fonctionnalités imposées par HOPEX :

- taxonomie Preferred/Allowed/Tolerated/Deprecated/Prohibited ;
- Platform Service Card ;
- Failure Domain Matrix ;
- GreenOps scorecard ;
- runbook DR MayaBank ;
- Technology Radar ;
- modèle de maturité ;
- matrices MayaBank ;
- ordre des waves de migration.

Ce sont des pratiques d’architecture proposées.

# 13. Hypothèses MayaBank

Sont entièrement fictifs :

- noms des plateformes MayaBank ;
- topologies réseau ;
- technologies exactes du core ;
- stratégies de DR ;
- statuts de standards ;
- niveaux de criticité ;
- volumes et capacité ;
- seuils RTO/RPO ;
- choix de vendors non explicitement imposés.

# 14. Ce qui doit être vérifié chez un client

1. Version exacte HOPEX/Aquila.
2. Solutions/modules/licences actifs.
3. Métaclasses technologiques disponibles.
4. Modèle Platform/Deployment réellement configuré.
5. Intégration IT-Pedia activée ou non.
6. Source lifecycle officielle retenue.
7. CMDB et mécanismes de synchronisation.
8. Cloud inventory connectors éventuels.
9. Taxonomie de standards.
10. Owners.
11. Sites/régions/zones réels.
12. RTO/RPO validés.
13. DR réellement testé.
14. Outils d’observabilité et de sécurité.
15. Règles de confidentialité du repository.

# 15. Frontière copyright

Ce repository :

- résume des faits publics ;
- cite les pages officielles ;
- ne copie pas de documentation propriétaire de façon substantielle ;
- ne distribue aucun module Hopex ;
- ne distribue aucun contenu IT-Pedia sous licence ;
- utilise MayaBank pour les exemples originaux.
