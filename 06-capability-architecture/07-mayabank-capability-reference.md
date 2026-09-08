# 07 — MayaBank Capability Architecture Reference

## 1. Objectif

Cette référence fournit un modèle original et cohérent pour relier stratégie, capabilities, value streams, applications, data, technologies et initiatives.

## 2. Structure L0/L1

### Customer & Party
- Customer Identity Management
- Customer Profile Management
- Consent Management
- Customer Communication

### Accounts & Deposits
- Account Opening
- Account Maintenance
- Balance Management
- Account Servicing

### Payments
- Payment Initiation
- Payment Processing
- Payment Routing
- Payment Settlement Coordination
- Payment Exception Handling
- Payment Reconciliation
- Payment Investigation
- Payment Reporting

### Fraud Management
- Fraud Monitoring
- Fraud Detection
- Fraud Decisioning
- Fraud Investigation
- Fraud Case Management

### Risk & Compliance
- Risk Assessment
- Compliance Monitoring
- Policy Management
- Control Management
- Regulatory Reporting

### Data & Analytics
- Data Governance
- Data Quality Management
- Master Data Management
- Analytical Data Provisioning
- AI/ML Model Governance

### Integration
- API Management
- Event Streaming
- File & Batch Integration
- Integration Observability

### Technology Platform
- Container Platform Operations
- Database Platform Operations
- Identity Platform Operations
- Observability Platform Operations
- Resilience & Recovery

### Operations
- Incident Management
- Problem Management
- Change Enablement
- Service Continuity
- Operational Monitoring

## 3. Capabilities stratégiques 2026–2027

Pour le scénario MayaBank :

| Capability | Importance | Current | Target | Gap |
|---|---:|---:|---:|---:|
| Instant Payment Execution | 5 | 3 | 5 | 2 |
| Fraud Decisioning | 5 | 2 | 5 | 3 |
| API Management | 4 | 3 | 5 | 2 |
| Event Streaming | 4 | 3 | 4 | 1 |
| Data Quality Management | 4 | 2 | 4 | 2 |
| Resilience & Recovery | 5 | 3 | 5 | 2 |
| Observability Platform Operations | 4 | 2 | 4 | 2 |

## 4. Capability → Application

### Instant Payment Execution
- Payment Orchestrator
- Payment Ledger
- Fraud Decision Service
- Customer Notification Service

### Fraud Decisioning
- Fraud Decision Service
- Feature Platform
- Customer & Transaction Data Services

### API Management
- API Gateway
- Developer Portal
- API Security Services

### Event Streaming
- Event Streaming Platform
- Schema Registry
- Connector Services

## 5. Capability → Data

### Instant Payment Execution
- Payment Instruction
- Account
- Beneficiary
- Settlement Status

### Fraud Decisioning
- Transaction
- Customer Identity
- Device Context
- Behavioural Features

### Regulatory Reporting
- Payment Events
- Customer
- Account
- Control Evidence

## 6. Capability → Technology

### Instant Payment Execution
- Container Platform
- Event Streaming Platform
- PostgreSQL Platform
- API Platform

### Fraud Decisioning
- Container Platform
- Feature Store / analytical platform
- Event Streaming Platform

### Resilience & Recovery
- Multi-site infrastructure
- Backup platform
- replication technology
- observability stack

## 7. Capability → Initiative

```text
Fraud Decisioning
→ Real-Time Fraud Modernization

Instant Payment Execution
→ Payment Platform Modernization

API Management
→ Enterprise API Governance

Resilience & Recovery
→ Multi-Site Resilience Program
```

## 8. Dependency chain example

```text
Strategic Outcome
Reduce payment rejection and fraud losses
        ↓
Capabilities
Instant Payment Execution + Fraud Decisioning
        ↓
Applications
Payment Orchestrator + Fraud Decision Service
        ↓
Platforms
OpenShift + Kafka + API Platform + Database
        ↓
Initiatives
Payment Modernization + Fraud Modernization
```

## 9. Heatmap interpretation

Priority 1 : Fraud Decisioning, Resilience & Recovery.  
Priority 2 : Instant Payment Execution, API Management, Data Quality.  
Priority 3 : Event Streaming and supporting capabilities already near target.

## 10. Executive view

Un board ne doit pas voir toute la taxonomie. Il doit voir :

- 10–20 capabilities déterminantes ;
- importance ;
- maturity gap ;
- investment ;
- top dependencies ;
- target date ;
- expected outcomes.

## 11. Domain view

Un domain architect peut descendre à L2/L3 et analyser :

- application coverage ;
- data dependencies ;
- technology risk ;
- overlaps ;
- projects ;
- owner/steward.

## 12. Rule of change

Toute modification significative de la taxonomie MayaBank doit documenter :

- raison ;
- impact sur children ;
- impact sur mappings ;
- impact sur reports/heatmaps ;
- owner approver ;
- effective date.