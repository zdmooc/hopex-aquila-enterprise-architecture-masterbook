# 11 — MayaBank Business Architecture Reference

## 1. Objectif

Ce chapitre assemble les concepts de la Partie V dans un modèle cohérent et réutilisable pour les futures parties HOPEX.

Le domaine de référence est **Instant Payments**.

## 2. Stakeholders

```text
Retail Customer
Merchant
Payments Business Director
Payments Operations
Fraud & Risk
Compliance
CIO
Enterprise Architecture
Platform Engineering
Payment Scheme
Regulator
```

## 3. Drivers

```text
D1 Instant payment adoption
D2 24x7 customer expectation
D3 Regulatory pressure
D4 Fraud pressure
D5 Legacy obsolescence
D6 High operations cost
D7 Slow change lead time
```

## 4. Outcomes

```text
O1 Payment confirmation P95 < 5 sec
O2 24x7 resilient payment execution
O3 Straight-through processing > 98%
O4 Manual exception handling < 5%
O5 Critical legacy dependencies reduced
O6 Regulatory traceability improved
```

## 5. Capability Map

```text
Payments
├─ Payment Product Management
├─ Payment Initiation
├─ Payment Orchestration
│  ├─ Payment Validation
│  ├─ Payment Routing
│  └─ Payment Status Management
├─ Fraud Decisioning
├─ Payment Clearing
├─ Payment Operations
│  ├─ Exception Management
│  └─ Payment Investigation
├─ Customer Notification
└─ Regulatory Reporting
```

Support capabilities :

```text
Customer Identity Management
API Management
Event Distribution
Observability
Platform Operations
Data Governance
Security Management
```

## 6. Value Stream

```text
Initiate
→ Validate
→ Decide
→ Execute
→ Confirm
→ Operate/Resolve if exception
```

### Stage outcomes

```text
Initiate  : valid request captured
Validate  : instruction is complete/authenticated
Decide    : risk and routing decision obtained
Execute   : funds movement instruction executed
Confirm   : final status visible to customer
Operate   : exception restored or investigated
```

## 7. Customer Journey

```text
Need to pay
→ choose beneficiary
→ enter amount
→ authenticate
→ wait for result
→ receive confirmation
→ inspect status if needed
```

Pain points current :

- uncertain status after timeout ;
- delayed notification ;
- repeated authentication on exception ;
- support lacks end-to-end transaction view.

## 8. Business Services

```text
Instant Payment Service
Payment Status Service
Beneficiary Verification Service
Payment Investigation Service
Customer Notification Service
```

## 9. Products / Offerings

```text
Retail Instant Payment Offering
Business Instant Payment Offering
Partner Payment API Offering
```

Each offering consumes a subset of the canonical business services.

## 10. Process Architecture

```text
Manage Payments
├─ Execute Instant Payment
│  ├─ Validate Payment Order
│  ├─ Authenticate Customer
│  ├─ Decide Fraud Risk
│  ├─ Route Payment
│  ├─ Execute Payment
│  └─ Confirm Payment
├─ Operate Payments
│  ├─ Handle Payment Exception
│  ├─ Investigate Payment
│  └─ Reconcile Payment
└─ Govern Payments
   ├─ Manage Payment Product
   ├─ Manage Scheme Compliance
   └─ Review Payment Performance
```

## 11. Organization

```text
Payments
├─ Payment Product Management
├─ Payment Engineering
└─ Payment Operations

Risk
└─ Fraud Management

Technology
└─ Platform Engineering

Data
└─ Data Governance
```

Ownership :

```text
Payment Product Management
→ Instant Payment Offering
→ Instant Payment Service

Payments Business Director
→ Payment Orchestration capability

Fraud Management
→ Fraud Decisioning capability

Payment Operations
→ Handle Payment Exception process

Platform Engineering
→ Event Distribution support capability
```

## 12. Business Information

```text
Customer
Account
Beneficiary
Payment Order
Payment Instruction
Fraud Decision
Payment Status
Payment Confirmation
Investigation Case
Settlement Position
```

## 13. Policies

```text
P1 Every instant payment must reach an explicit final status.
P2 High-risk instructions require enhanced fraud controls.
P3 Critical payment events must be auditable.
P4 Sensitive payment information follows enterprise retention/privacy policy.
P5 24x7 service requires tested recovery capabilities.
```

## 14. Application Support Mapping

```text
Payment Orchestrator
→ Payment Orchestration
→ Execute Instant Payment
→ Instant Payment Service

Fraud Engine
→ Fraud Decisioning
→ Decide Fraud Risk

Operations Portal
→ Payment Operations
→ Handle Payment Exception

Notification Service
→ Customer Notification
→ Confirm Payment
```

## 15. Technology Support

```text
OpenShift Platform
→ Payment Orchestrator runtime

Event Streaming Platform
→ Event Distribution
→ status/fraud/notification event flows

Identity Platform
→ Customer Identity Management

Observability Platform
→ Operational Monitoring
```

## 16. Current State

```text
Capabilities
Payment Orchestration maturity = 2/5
Payment Operations maturity    = 2/5
Fraud Decisioning maturity     = 4/5

Processes
manual exception handling
multiple operational handoffs

Applications
legacy coupling
point-to-point interfaces

Technology
single-site dependencies on selected components
```

## 17. Target State

```text
Capabilities
orchestration 5/5
operations 4/5
fraud 5/5
observability 4/5

Value Stream
real-time + transparent status

Operating Model
product/domain ownership
exception-oriented operations
shared platforms

Architecture
API + event-driven integration
resilient runtime
standardized observability
```

## 18. Gaps

```text
G1 no canonical end-to-end payment status model
G2 excessive point-to-point coupling
G3 manual exception handling
G4 incomplete observability
G5 inconsistent service ownership
G6 legacy technology dependencies
G7 insufficient multi-site recovery
```

## 19. Initiatives

```text
I1 Canonical Payment Repository & Ownership
I2 Payment API Rationalization
I3 Payment Event Backbone
I4 Payment Status Model
I5 Operations Automation
I6 Multi-site Runtime Resilience
I7 Legacy Decommissioning
```

## 20. Traceability example

```text
Driver
24x7 customer expectation
↓
Outcome
resilient payment execution
↓
Capability
Payment Orchestration
↓
Value Stage
Execute / Confirm
↓
Business Service
Instant Payment Service
↓
Process
Execute Instant Payment
↓
Application
Payment Orchestrator
↓
Technology
OpenShift + Event Streaming
↓
Initiatives
Payment Event Backbone + Multi-site Runtime
```

## 21. Views to build in HOPEX

1. MayaBank Business Context
2. Payments Capability Map
3. Instant Payment Value Stream
4. Instant Payment Customer Journey
5. Business Service Catalog
6. Process Architecture
7. Capability × Application Matrix
8. Capability × Organization Matrix
9. Business Information Map
10. Current/Target Capability Heatmap
11. Gap Map
12. Business Transformation Roadmap

## 22. Rule for the rest of the masterbook

The names above become canonical pedagogical objects. Future parts should reuse them rather than invent parallel names.

This is essential for demonstrating how a real HOPEX repository gains value through shared identity and cross-domain traceability.