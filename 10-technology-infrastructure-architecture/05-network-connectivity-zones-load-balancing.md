# 05 — Network, connectivity, zones et load balancing

## 1. Pourquoi le réseau est un objet d’architecture

Le réseau matérialise les chemins de communication entre utilisateurs, applications, plateformes, données et partenaires.

Il permet d’analyser :

- exposition ;
- segmentation ;
- latency ;
- dépendances ;
- SPOF ;
- sécurité ;
- résilience inter-site ;
- flux hybrides.

## 2. Zones

Exemple MayaBank :

```text
Internet / Partner
DMZ / Edge
Application Zone
Data Zone
Management Zone
DR Site / Secondary Region
```

Les noms et règles réelles dépendent du client.

## 3. North-South vs East-West

```text
North-South
external ↔ platform/application

East-West
application/service ↔ application/service
```

Cette distinction aide à choisir contrôles, gateways et observabilité.

## 4. Connectivity objects

Le niveau d’EA peut retenir :

- network zone ;
- major network link ;
- gateway ;
- load balancer ;
- firewall boundary ;
- proxy ;
- DNS dependency ;
- external connectivity.

Éviter de reproduire chaque règle firewall.

## 5. Load balancing

Un load balancer peut agir :

- L4 ;
- L7 ;
- global ;
- régional ;
- cluster ingress ;
- application-specific.

Questions :

- health checks ?
- session affinity ?
- failover ?
- TLS termination ?
- multi-site routing ?

## 6. DNS

DNS est souvent une dépendance transversale critique.

Analyser :

```text
resolver
authoritative zones
TTL
failover behavior
private/public split
DR implications
```

## 7. Firewalls et segmentation

L’EA doit montrer les **trust boundaries** et politiques structurantes, pas chaque ACL.

Exemple :

```text
Digital Channel
→ API Edge
→ Payment Zone
→ Core/Data Zone
```

## 8. API Gateway

L’API Gateway est un composant/service de contrôle applicatif :

- authentication/authorization integration ;
- routing ;
- throttling ;
- policy enforcement ;
- observability ;
- lifecycle/version exposure.

API Gateway ≠ load balancer uniquement.

## 9. Service Mesh

Peut fournir selon implémentation :

- service-to-service identity ;
- mTLS ;
- routing ;
- retries ;
- telemetry ;
- policy.

Ne pas l’introduire sans besoin : il ajoute complexité et responsabilités opérationnelles.

## 10. Hybrid connectivity

Options :

```text
VPN
private link
leased line
cloud interconnect
internet + secure tunnel
```

Décisions : débit, latency, availability, encryption, routing, cost.

## 11. Partner connectivity

Pour clearing ou partenaires :

- endpoint ownership ;
- protocol ;
- certificates ;
- network path ;
- active/standby ;
- timeout ;
- monitoring ;
- escalation.

## 12. Network dependency map

```text
Payment Orchestrator
→ cluster network
→ egress gateway
→ partner link
→ Clearing Network
```

Un seul egress point peut être un SPOF même si l’application est multi-replica.

## 13. Network latency budget

Le budget end-to-end peut être décomposé :

```text
Client edge
+ API gateway
+ service hops
+ DB
+ partner network
```

Pour un paiement instantané, le budget doit rester compatible avec l’objectif end-to-end.

## 14. Multi-site routing

Documenter :

- active/active ou active/passive ;
- DNS/global LB ;
- session/state implications ;
- data replication ;
- split-brain controls ;
- recovery runbook.

## 15. Security controls

- TLS ;
- mTLS where justified ;
- certificate lifecycle ;
- firewall policy ;
- ingress/egress control ;
- network policy ;
- DDoS/WAF at exposed boundaries where applicable.

## 16. MayaBank target connectivity

```text
Customer
→ Edge/WAF
→ API Management
→ OpenShift ingress
→ Payment services
→ Core / Fraud / Clearing

Events
→ Kafka platform

Admin
→ Management Zone
```

## 17. Anti-patterns

- diagramme réseau = liste d’IP ;
- firewall rules dans l’EA repository ;
- aucune zone de confiance ;
- HA applicative avec unique LB ;
- multi-region sans DNS/failover design ;
- retries réseau sans budget ni idempotency.

## 18. Questions d’entretien

**Pourquoi DNS doit-il apparaître dans certains modèles ?**  
Parce qu’il peut être une dépendance commune et un mécanisme de bascule critique.

**Pourquoi ne pas stocker toutes les ACL dans HOPEX ?**  
Parce qu’elles appartiennent à des outils d’exploitation/configuration ; HOPEX conserve les frontières et dépendances utiles à l’architecture.
