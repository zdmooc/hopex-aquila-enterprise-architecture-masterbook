# 05 — Scenario Analysis, Investment Prioritization et Capability Roadmaps

## 1. De la carte à la décision

Une Capability Architecture devient réellement utile quand elle permet de comparer des scénarios et d'allouer les investissements.

Chaîne de raisonnement :

```text
Strategic Driver
→ Capability Importance
→ Current Assessment
→ Target Assessment
→ Gap
→ Options / Scenarios
→ Investments
→ Roadmap
→ Outcome
```

## 2. Scénario A — Moderniser localement

Exemple MayaBank : conserver l'orchestrateur existant et renforcer fraude, observabilité et résilience.

Avantages :

- changement plus limité ;
- time-to-value court ;
- moins de migration initiale.

Limites :

- dette structurelle conservée ;
- coûts d'exploitation potentiellement élevés ;
- capacité de transformation limitée.

## 3. Scénario B — Plateforme cible

Construire une nouvelle plateforme de paiement cible puis migrer progressivement.

Avantages :

- architecture plus cohérente ;
- meilleure scalabilité ;
- réduction de dette à terme.

Risques :

- coexistence longue ;
- migration de données et flux ;
- dépendances cross-domain ;
- investissement initial plus élevé.

## 4. Scénario C — Rationalisation forte

Réduire le nombre d'applications supportant des capabilities similaires.

Décision basée sur :

- business value ;
- health ;
- cost ;
- risk ;
- capability coverage ;
- replacement feasibility.

## 5. Modèle de scoring pédagogique

```text
Investment Priority =
  0.30 × Strategic Importance
+ 0.25 × Maturity Gap
+ 0.20 × Risk
+ 0.15 × Technology Obsolescence
+ 0.10 × Regulatory/Urgency factor
```

Le poids réel doit être défini par le client.

## 6. Ne pas confondre priorité et budget

Une capability peut être prioritaire mais nécessiter :

- exploration ;
- architecture work ;
- organisation ;
- data remediation ;
- changement de processus ;

et pas seulement un budget IT.

## 7. Capability Roadmap

Une roadmap doit montrer la progression de l'aptitude, pas seulement les dates projet.

```text
2026 H2
Fraud Decisioning maturity 2 → 3
- feature store baseline
- decision API standard
- observability

2027 H1
3 → 4
- real-time enrichment
- HA multi-site
- automated model governance

2027 H2
4 → 5
- closed-loop optimization
- advanced analytics
```

## 8. Transitional states

Une capability peut changer via plusieurs états :

```text
Current
→ Stabilized
→ Partially Modernized
→ Target
```

Les applications et technologies supportantes peuvent donc varier par étape.

## 9. Portfolio view

Au niveau exécutif, afficher :

- capabilities stratégiques ;
- maturity gaps ;
- investissements associés ;
- dépendances critiques ;
- delivery confidence ;
- expected outcome.

## 10. Kill criteria

Une initiative ne doit pas continuer uniquement parce qu'elle existe. Définir des critères d'arrêt si :

- le gap n'existe plus ;
- l'option cible change ;
- une dépendance rend le scénario non viable ;
- le coût dépasse la valeur ;
- une autre initiative couvre déjà la capability.

## 11. Architecture Board

Le board doit challenger :

1. la capability cible ;
2. la preuve du gap ;
3. les options étudiées ;
4. les impacts ;
5. les dependencies ;
6. le target state ;
7. les indicateurs de résultat.

## 12. Outcome tracking

Après mise en œuvre :

```text
Investment
→ Delivered change
→ Capability maturity change
→ Business outcome
```

Sans mesure post-implementation, la capability roadmap reste un exercice de planification non bouclé.