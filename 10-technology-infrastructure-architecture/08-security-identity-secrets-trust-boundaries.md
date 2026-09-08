# 08 — Security Architecture, Identity, Secrets & Trust Boundaries

## 1. Security by architecture

La sécurité technique doit être intégrée aux objets et flux plutôt qu’ajoutée comme une liste générique de contrôles.

Questions :

- qui s’authentifie ?
- qui autorise ?
- quelles zones de confiance ?
- quels secrets ?
- quelles données sensibles ?
- quelles surfaces d’exposition ?
- quelles dépendances PKI ?
- quelles traces d’audit ?

## 2. Identity planes

Distinguer :

```text
Human identity
Service identity
Machine/node identity
Administrative identity
External partner identity
```

Les mécanismes peuvent différer.

## 3. Authentication vs authorization

```text
Authentication
Who are you?

Authorization
What may you do?
```

Un token valide ne signifie pas automatiquement que l’action est autorisée.

## 4. Federation

Patterns :

- OIDC ;
- SAML ;
- enterprise directory ;
- workload identity ;
- partner federation.

Les protocoles doivent être alignés au cas d’usage.

## 5. Service-to-service identity

Options :

- OAuth2 client credentials ;
- mTLS ;
- workload identity ;
- signed tokens ;
- service mesh identity.

Éviter les credentials partagés statiques.

## 6. Secrets management

Secrets :

- API keys ;
- passwords ;
- private keys ;
- certificates ;
- database credentials.

Architecture cible :

```text
central secret service
→ controlled distribution
→ rotation
→ audit
→ revocation
```

## 7. Certificate lifecycle

Une expiration de certificat peut provoquer une panne globale.

Documenter :

- issuer ;
- scope ;
- expiration monitoring ;
- rotation ;
- trust chain ;
- DR availability.

## 8. Trust boundaries

Exemple :

```text
Internet
| boundary |
Edge/API Zone
| boundary |
Application Zone
| boundary |
Core/Data Zone
```

Chaque traversée implique contrôles et observabilité.

## 9. Network security

- firewalls ;
- network policies ;
- ingress/egress control ;
- WAF where exposed ;
- segmentation ;
- secure admin paths.

## 10. Platform security

Pour OpenShift/Kubernetes :

- RBAC ;
- namespace isolation ;
- service accounts ;
- admission policies ;
- image security ;
- secrets ;
- network policies ;
- audit logs.

## 11. Supply-chain security

```text
Source
→ Build
→ Dependencies
→ Image
→ Registry
→ Deployment
```

Contrôles possibles : signatures, scanning, provenance, approved registries.

## 12. Encryption

### In transit
TLS/mTLS selon flux.

### At rest
storage/database encryption selon classification et politique.

### Keys
ownership, rotation, backup, access, revocation.

## 13. Privileged access

Accès d’administration :

- strong authentication ;
- least privilege ;
- bastion/PAM where applicable ;
- logging ;
- emergency access ;
- review.

## 14. Logging security events

Événements :

- authentication failures ;
- privilege changes ;
- secret access ;
- policy violations ;
- anomalous network activity ;
- deployment changes.

## 15. Shared responsibility matrix

| Layer | Platform Team | App Team | Security |
|---|---|---|---|
| Cluster hardening | R | I | C/A policy |
| App authz | C | R/A | C |
| Secrets platform | R | C | C |
| Data classification | I | C | C with Data Owner |
| Incident response | R | R | A/C depending model |

## 16. MayaBank security chain

```text
Customer auth
→ API token
→ API Management policies
→ service identity
→ payment authorization
→ encrypted partner flow
→ immutable/auditable traces
```

## 17. Security anti-patterns

- shared admin account ;
- secret dans Git ;
- long-lived credentials ;
- service identity = human account ;
- flat network ;
- certificate rotation manuelle non surveillée ;
- logs contenant secrets/PII ;
- DR sans accès aux clés.

## 18. Questions d’entretien

**Pourquoi la PKI est-elle une dépendance de résilience ?**  
Parce que certificats, validation et renouvellement peuvent conditionner presque tous les flux sécurisés.

**Pourquoi le réseau seul ne suffit-il pas au Zero Trust ?**  
Parce que l’identité, l’autorisation, le contexte, la posture et la vérification continue complètent la segmentation réseau.
