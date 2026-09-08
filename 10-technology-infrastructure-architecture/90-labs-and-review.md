# 90 — Labs pratiques et questions de contrôle

## 1. Objectif

Ces labs transforment la Partie X en exercices de mission. Ils peuvent être réalisés dans HOPEX si un environnement est disponible ou en Markdown/draw.io en conservant la logique de repository.

# 2. Labs

## Lab 01 — Technology Catalog
Construire un catalogue de 20 technologies MayaBank avec family, owner, lifecycle et standard status.

**Livrable :** Technology Catalog.

## Lab 02 — Product vs Platform
Pour OpenShift, Kafka, PostgreSQL et IAM, distinguer produit, version, managed platform et deployment instance.

**Contrôle :** aucune application ne doit être confondue avec une technologie.

## Lab 03 — Application × Platform Matrix
Mapper les 12 applications MayaBank de la Partie VIII vers leurs plateformes principales.

## Lab 04 — Platform × Technology Matrix
Relier OpenShift Platform, Event Streaming, API Management, DB Platform et Observability aux produits qui les réalisent.

## Lab 05 — Technology Standards
Attribuer Preferred / Allowed / Tolerated / Deprecated / Prohibited à 15 technologies et justifier chaque décision.

## Lab 06 — IT-Pedia Impact Scenario
Simuler la réception d’une nouvelle date d’EOL pour un produit et produire la chaîne d’impact jusqu’aux applications/processus.

## Lab 07 — OpenShift Logical Architecture
Dessiner control plane, worker pools, ingress, storage, identity, observability et principaux failure domains.

## Lab 08 — Namespace Governance
Définir une stratégie namespaces/quotas/network policies pour Payments, Fraud et Shared Services.

## Lab 09 — Capacity Model
Construire un modèle Business Load → Workload → Requests/Limits → Cluster Capacity avec une marge de panne.

## Lab 10 — Network Zones
Dessiner External, Edge, Application, Data/Core, Management et DR avec les principaux flux.

## Lab 11 — Load Balancer SPOF
Partir d’une architecture applicative HA et démontrer comment un load balancer unique annule une partie de la résilience.

## Lab 12 — Hybrid Connectivity
Comparer VPN, private link/interconnect et internet sécurisé pour une connexion cloud ↔ core banking.

## Lab 13 — Storage Architecture
Mapper block/file/object/DB-managed storage aux workloads MayaBank.

## Lab 14 — Backup vs Replication
Construire une matrice de scénarios : node loss, site loss, logical corruption, ransomware, accidental deletion.

## Lab 15 — RTO/RPO Matrix
Définir des objectifs pédagogiques pour Payment, Fraud, Notification, Reconciliation, Observability et Analytics.

## Lab 16 — Failure Domain Analysis
Tracer : pod → node → cluster → site → region et identifier les dépendances communes qui restent hors de cette chaîne.

## Lab 17 — DR Dependency Order
Construire le runbook logique Network/DNS → IAM/PKI → Storage/DB → Platform → Messaging/API → Applications → Partners.

## Lab 18 — Security Trust Boundaries
Cartographier authentication, authorization, service identity, secrets, certificates et zones de confiance.

## Lab 19 — Certificate Expiry Scenario
Simuler l’expiration d’un certificat de clearing et produire impact, detection, mitigation et prévention.

## Lab 20 — Observability Architecture
Définir metrics/logs/traces pour le processus Execute Instant Payment avec corrélation end-to-end.

## Lab 21 — Capacity Under Failure
Vérifier si la plateforme peut absorber la charge après perte d’un worker pool ou d’un site.

## Lab 22 — Technology Obsolescence
Choisir cinq technologies legacy fictives, construire leur blast radius et prioriser les remédiations.

## Lab 23 — Current / Transition / Target
Produire quatre vues : VM-heavy current → foundations → platform migration → target.

## Lab 24 — Architecture Board
Préparer une page avec current, critical path, SPOF, EOL, target, transition, risques, décisions et roadmap.

# 3. Questions corrigées

## Q01
Quelle différence entre Technology Product et Platform ?

**Réponse :** le produit est une technologie/vendor release ; la plateforme est un service exploité combinant produits, configuration, opérations et contrats de consommation.

## Q02
Pourquoi une application ne doit-elle pas être modélisée comme un cluster ?

**Réponse :** l’application est un actif logique avec responsabilité métier/IT ; le cluster est une plateforme ou instance d’exécution.

## Q03
Qu’est-ce qu’un failure domain ?

**Réponse :** un ensemble de composants susceptibles d’être affectés simultanément par une même panne.

## Q04
Trois replicas garantissent-ils la HA ?

**Réponse :** non, s’ils partagent un même node, storage backend, site ou autre dépendance commune.

## Q05
Pourquoi distinguer produit et version ?

**Réponse :** le lifecycle, les vulnérabilités et le support peuvent varier selon la version alors que l’identité du produit reste stable.

## Q06
Preferred signifie-t-il Supported ?

**Réponse :** non. Preferred exprime une décision interne ; Supported peut uniquement refléter le support vendor.

## Q07
Quel rôle peut jouer IT-Pedia dans HOPEX ?

**Réponse :** fournir/aligner/mettre à jour des informations technologiques et lifecycle afin d’aider l’analyse d’obsolescence ; la gouvernance interne reste nécessaire.

## Q08
Pourquoi une evidence date est-elle importante ?

**Réponse :** parce que les dates et statuts de support évoluent et doivent être auditables.

## Q09
Quel est le danger d’une plateforme partagée ?

**Réponse :** elle concentre le blast radius et les dépendances, même si elle apporte standardisation et efficacité.

## Q10
Namespace = application ?

**Réponse :** non. Un namespace est une unité de segmentation/gouvernance runtime ; plusieurs stratégies de mapping sont possibles.

## Q11
Pourquoi modéliser DNS ?

**Réponse :** parce qu’il peut être une dépendance commune et un mécanisme critique de résolution ou de bascule.

## Q12
Quelle différence entre North-South et East-West ?

**Réponse :** North-South décrit les flux entrant/sortant de la plateforme ; East-West décrit les communications internes entre services/workloads.

## Q13
API Gateway = load balancer ?

**Réponse :** non. Un API Gateway peut gérer policies, auth, throttling, lifecycle et observabilité au-delà du simple équilibrage.

## Q14
Pourquoi un service mesh peut-il être un anti-pattern ?

**Réponse :** s’il est ajouté sans besoin justifié, il augmente fortement complexité et coût opérationnel.

## Q15
Quel est le problème d’un réseau plat ?

**Réponse :** il réduit l’isolation, augmente le blast radius et rend plus difficile l’application de trust boundaries.

## Q16
Backup et réplication sont-ils équivalents ?

**Réponse :** non. La réplication protège surtout la disponibilité du présent ; le backup permet de restaurer un état historique indépendant.

## Q17
Snapshot = backup ?

**Réponse :** pas automatiquement. Il faut vérifier indépendance, rétention, immutability, restore et résilience au site loss.

## Q18
Qu’est-ce que le RPO ?

**Réponse :** la perte de données maximale acceptable exprimée dans le temps.

## Q19
Qu’est-ce que le RTO ?

**Réponse :** le délai maximal acceptable pour restaurer le service.

## Q20
Pourquoi tester les restores ?

**Réponse :** parce qu’un backup existant mais non restaurable ne fournit pas la protection attendue.

## Q21
HA et DR sont-ils la même chose ?

**Réponse :** non. HA traite surtout les pannes locales et continuité ; DR traite la reprise après une perte majeure.

## Q22
Active/active est-il toujours supérieur à active/passive ?

**Réponse :** non. Il peut réduire le temps de bascule mais ajoute complexité de state, consistency, routing et exploitation.

## Q23
Pourquoi le failback doit-il être testé ?

**Réponse :** revenir au site nominal est une opération risquée différente du failover.

## Q24
Qu’est-ce qu’un retry storm ?

**Réponse :** une multiplication de retries qui aggrave la saturation d’un service défaillant.

## Q25
Authentication et authorization sont-elles interchangeables ?

**Réponse :** non. Authentication établit l’identité ; authorization décide ce qu’elle peut faire.

## Q26
Pourquoi les certificats font-ils partie de la résilience ?

**Réponse :** leur expiration ou indisponibilité peut interrompre des flux critiques même si compute et applications fonctionnent.

## Q27
Pourquoi éviter les secrets dans Git ?

**Réponse :** parce qu’ils deviennent difficiles à révoquer, peuvent fuiter dans l’historique et échappent à un secret lifecycle approprié.

## Q28
Quels sont les trois piliers classiques de l’observabilité ?

**Réponse :** metrics, logs et traces.

## Q29
Monitoring et observability sont-ils identiques ?

**Réponse :** non. Monitoring surveille surtout des conditions connues ; observability aide à comprendre des comportements non prévus à partir des signaux.

## Q30
Que sont les golden signals ?

**Réponse :** latency, traffic, errors et saturation, base fréquente pour observer un service.

## Q31
Pourquoi capacity planning doit-il intégrer la panne ?

**Réponse :** la plateforme doit conserver assez de marge pour absorber la charge après perte d’une partie de sa capacité.

## Q32
Pourquoi 100 % d’utilisation est-il dangereux ?

**Réponse :** il ne reste aucune marge pour burst, maintenance, croissance ou panne.

## Q33
Qu’est-ce qu’une architecture transition ?

**Réponse :** un état intermédiaire explicitant coexistence, dépendances et risques entre current et target.

## Q34
Pourquoi le dual-run est-il risqué ?

**Réponse :** il augmente coûts, ambiguity de routage, risques de divergence de données et complexité opérationnelle.

## Q35
Que faut-il retirer lors d’un decommission ?

**Réponse :** compute mais aussi DNS, flux réseau, certificats, stockage, backups, monitoring, licences et relations de repository.

## Q36
Qu’est-ce que le technical debt item ?

**Réponse :** un risque ou écart technologique documenté avec impact, owner, mitigation et cible de remédiation.

## Q37
HOPEX doit-il contenir chaque VM et chaque pod ?

**Réponse :** non par principe. Il doit garder la granularité nécessaire à l’analyse d’architecture, avec liens vers CMDB/outils runtime lorsque nécessaire.

## Q38
Pourquoi GreenOps doit-il respecter la résilience ?

**Réponse :** réduire trop fortement la capacité ou la redondance peut compromettre HA, maintenance et reprise.

## Q39
Quel est le meilleur point de départ d’une mission infrastructure ?

**Réponse :** identifier le service métier/applicatif critique, ses plateformes, son chemin d’exécution et ses dépendances avant de détailler tous les actifs.

## Q40
Quelle question finale doit être posée devant une Architecture Board ?

**Réponse :** quels scénarios de panne, d’obsolescence ou de transition ne sont toujours pas correctement couverts, et quel impact métier en résulte ?
