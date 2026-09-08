# 06 — BIAN, Industry Reference Models et MayaBank

## 1. Pourquoi utiliser un modèle de référence

Un modèle de référence accélère le cadrage mais ne doit jamais être copié comme architecture cible sans adaptation.

Utilités :

- vocabulaire commun ;
- benchmark ;
- couverture initiale ;
- détection d'oubli ;
- comparaison entre domaines ;
- accélération des ateliers.

## 2. BIAN et HOPEX

Le Store MEGA publie un module **ITPM BIAN Capability Maps** qui convertit des contenus BIAN ArchiMate en Business Capability Maps HOPEX. La documentation précise que les données BIAN doivent être obtenues auprès du standardization body et qu'un accès/membership peut être requis selon le contenu.

Cela confirme deux points :

1. HOPEX sait exploiter des capability maps issues d'un modèle bancaire externe ;
2. le contenu BIAN reste soumis à ses propres conditions de licence.

## 3. Règle de ce masterbook

Ce dépôt ne recopie pas la taxonomie BIAN propriétaire/membre.

Nous utilisons :

- des noms génériques de capabilities bancaires ;
- un modèle MayaBank original ;
- des références vers la source officielle BIAN/MEGA pour aller plus loin.

## 4. Import ≠ adoption

Même si un framework est importé :

```text
Reference capability
≠ automatiquement
Enterprise capability canonique
```

Il faut décider :

- conserver ;
- renommer ;
- mapper ;
- fusionner ;
- exclure ;
- spécialiser.

## 5. Mapping de référence

Approche recommandée :

```text
Industry Reference Model
       ↓ mapping
Enterprise Capability Model
       ↓ ownership
Domain Capability Model
       ↓ assessments
Application/Data/Technology mappings
```

## 6. MayaBank — L0 original

```text
Customer & Party
Accounts & Deposits
Payments
Risk & Compliance
Fraud Management
Data & Analytics
Integration
Technology Platform
Operations
Finance & Performance
```

## 7. Exemple Payments

```text
Payments
├─ Payment Initiation
├─ Payment Processing
├─ Payment Routing
├─ Payment Settlement Coordination
├─ Payment Exception Handling
├─ Payment Reconciliation
├─ Payment Investigation
└─ Payment Reporting
```

## 8. Exemple Fraud Management

```text
Fraud Management
├─ Fraud Monitoring
├─ Fraud Detection
├─ Fraud Decisioning
├─ Fraud Investigation
└─ Fraud Case Management
```

## 9. Exemple Technology Platform

```text
Technology Platform
├─ Container Platform Operations
├─ Event Streaming
├─ API Platform Operations
├─ Identity Platform Operations
├─ Observability
├─ Database Platform Operations
└─ Resilience & Recovery
```

## 10. Vérification avec un modèle externe

Lors d'un atelier :

1. produire d'abord le modèle interne ;
2. comparer avec un framework externe ;
3. identifier les gaps ;
4. discuter les écarts ;
5. décider explicitement ce qui est retenu.

Cela évite que le modèle externe dicte artificiellement l'organisation de l'entreprise.

## 11. Traceability

Conserver :

```text
Enterprise capability ID
Reference model name
Reference capability ID/name
Mapping type
Mapping confidence
Review date
```

## 12. Entretien

**Pourquoi utiliser BIAN avec HOPEX ?**  
Pour accélérer le cadrage bancaire et comparer la couverture du capability model, tout en conservant un modèle d'entreprise gouverné et adapté au contexte.

**Pourquoi ne pas copier BIAN tel quel ?**  
Parce qu'un industry model n'est ni l'organisation, ni le portefeuille applicatif, ni la stratégie réelle du client ; il sert de référence, pas de vérité d'entreprise.