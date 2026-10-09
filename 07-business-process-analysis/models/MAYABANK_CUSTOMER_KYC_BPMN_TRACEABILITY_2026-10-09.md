# S3 — BPMN 2.0 Customer/KYC : modèle, contrôles et correspondances SI

**Date : 2026-10-09** · **Statut : REFERENCE_MODEL / NOT_RUNTIME_EXECUTED**  
**Fichier BPMN standard :** [Mayabank Customer/KYC Onboarding](mayabank-customer-kyc-onboarding-soluxan-2026-10-09.bpmn)  
**Lecture requise :** il s'agit d'un modèle pédagogique de **domaine Customer/KYC**, et non d'un processus réel d'une banque, d'une exportation native HOPEX, ni d'un workflow déployé Camunda/Pega.

## Scope métier et frontières

**Déclencheur** : réception d'une intention d'entrée en relation prospect.  
**Fins** : Customer confirmé dans le core, KYC rejeté, ou dossier en attente/exception gouvernée.  
**Hors scope** : consentements non réglementairement exigés, traitements ultérieurs Selfcare, Customer360 matérialisé, moteurs KYC propriétaires, relation interbancaire, et exécution par un moteur BPM.

Les étapes suivent le modèle de [MayaBank Customer I03](https://github.com/zdmooc/mayabank-customer-identity-kyc-digital-banking-architecture/blob/main/docs/journeys/I03_PARCOURS_DIGITAUX.md) et la [matrice S1](https://github.com/zdmooc/mayabank-customer-identity-kyc-digital-banking-architecture/blob/main/docs/traceability/SOLUXAN_S1_EXIGENCES_PROCESSUS_APPLICATION_TESTS_2026-10-09.md).

## Mapping des activités BPMN

| BPMN id | Étape | FR/AC | Application de référence | Données manipulées | Contrôle principal | Owner rôle candidat |
|---|---|---|---|---|---|---|
| Task_Capture | Capturer le prospect | FR-01 / AC-01 | Onboarding + Party | prospect_id, customer_creation_id | pas de Customer prématuré | Product / Customer |
| Task_Identity | Vérifier identité | FR-02 / AC-02 | Onboarding + Identity Provider | evidence ref, identity status | réponse incertaine = attente | KYC Ops |
| Gateway_Identity / Task_RequestInfo | Traiter non-vérifié | FR-02/10 / AC-02/10 | KYC Case / Manual Review | case state | pas d'approbation implicite | Compliance |
| Task_Profile | Profil CDD/KYB | FR-03/04 / AC-03/04 | Relationship + KYC Case | UBO, mandate, purpose | complétude et provenance | KYC Owner |
| Task_Screening | Screening | FR-05 / AC-05 | KYC Case + Screening Provider | result, policy_version | REVIEW si ambigu | Compliance |
| Gateway_Screening / Task_ManualReview | Déterminer recours humain | FR-05/10 / AC-05/10 | Manual Review | reviewer/decision/evidence | reviewer habilité / SoD | KYC Operations |
| Task_Approve | Décision KYC | FR-05 / AC-05 | KYC Case | decision, audit | version policy et signature | Compliance |
| Task_Consent | Consentements de parcours | FR-06 / AC-06 | Consent Service | finalité, version, status | reconstitution historique | DPO / Customer |
| Task_CreateCustomer | Création core | FR-01/08 / AC-01/08 | Party Service + ACL/MQ/Core | stable customer_creation_id | idempotence et outbox | Application Architect + Core |
| Gateway_Core / Task_Inquiry | Timeout après écriture | FR-08/10 / AC-08/10 | Integration Adapter + Core | UNKNOWN, correlation_id | jamais retry aveugle | Core Owner / Ops |
| Gateway_Inquiry / Task_Repair | Statut toujours inconnu | FR-10 / AC-10 | Reconciliation + Manual Case | discrepancy, inquiry history | correction humaine gouvernée | Payment/Customer Ops |
| End_Created / End_Rejected / End_Pending | issue métier | FR-01/05/10 | KYC/Party + BPM case | état final ou pending | journal et corrélation | Product Owner |

## Variantes / exceptions et indicateurs

| Variante | Déclencheur | Comportement autorisé | KPI (formule, valeur réelle à établir) |
|---|---|---|---|
| Identité non résolue | vérification incomplète | `RequestInfo → Pending` | taux de dossiers en attente = pending / entrants |
| Screening ambigu | vendor résultat REVIEW | revue humaine habilitée | manual review ratio = dossiers en revue / dossiers |
| Rejet confirmé | reviewer rejet | `End_Rejected` avec motif auditable | rejected ratio = rejets / décisions |
| Timeout Core | réponse perdue | `Inquiry` et même clé de création | UNKNOWN ratio = cas incertains / demandes core |
| UNKNOWN persistant | inquiry sans preuve | exception pilotée `End_Pending` | durée de résolution des cas ouverts |
| Création confirmée après inquiry | confirmation externe tardive | converger vers `End_Created` sans création supplémentaire | duplication = 0 effet supplémentaire (critère, non mesure réelle) |

Aucun SLA/RTO/RPO/volume cible, chiffre d'acceptation et plan de contrôles client n'est présumé.

## RACI pédagogique

| Activité | Product Customer | KYC/Compliance | Data Owner | Architecte Solution | Dev/QA | Operations |
|---|---|---|---|---|---|---|
| Valider le parcours et ses issues | **A** | C | C | R | C | I |
| Approuver règles KYC et SoD | C | **A/R** | I | C | I | I |
| Statuer sur Customer mastership | C | C | **A** | R | C | C |
| Concevoir interfaces et inconnus | C | C | C | **A/R** | R | C |
| Construire/valider les tests | C | C | I | A | **R** | C |
| Définir replay et procédure de réparation | C | C | C | A | R | **R** |

**A/R** signifient responsabilité théorique en atelier MayaBank ; en mission, c'est le client qui nomme les propriétaires.

## Contrôles de validité de la représentation

- Le fichier `.bpmn` possède `definitions/process/sequenceFlow` et les éléments de **BPMN DI** (`BPMNShape/BPMNEdge`).
- Les gateways explicitent les cas `VERIFIED/UNRESOLVED`, `CLEAR/REVIEW`, `APPROVED/REJECTED/MORE_INFORMATION`, `ACK_CONFIRMED/TIMEOUT_UNKNOWN`, `CREATED_CONFIRMED/UNKNOWN_AFTER_INQUIRY`.
- `isExecutable=false` : aucune revendication d'exécution par un moteur ou import/validation HOPEX.
- **Validation technique** à distinguer : cohérence des identifiants et reachability du graphe vérifiables par inspection ; conformité XSD/import natif restant à confirmer si un outil BPMN autorisé est disponible.

## Entretien / revue d'architecture

1. D'abord expliquer le **processus et les issues métier** (5 minutes).
2. Puis montrer le **mapping processus ↔ applications / données / acteurs** (3 minutes).
3. Enfin résoudre les **exceptions core UNKNOWN, consent et revue humaine** (2 minutes).
4. Présenter l'alternative dans [S2 — dossier de choix](https://github.com/zdmooc/mayabank-customer-identity-kyc-digital-banking-architecture/blob/main/docs/decision/SOLUXAN_S2_DOSSIER_CHOIX_ARCHITECTURE_CUSTOMER_LEGACY_2026-10-09.md).

Le modèle formel ne remplace ni discovery, ni validation d'un vrai référentiel client, ni tests de workflow runtime.
