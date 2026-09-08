# 10 — Technology Lifecycle, Obsolescence, Standards & Technical Debt

## 1. Pourquoi le lifecycle technologique est critique

Une architecture peut être fonctionnelle tout en accumulant un risque important si ses composants technologiques arrivent en fin de support.

Questions :

- quelles versions sont hors support ?
- quelles technologies sont encore supportées mais non stratégiques ?
- quelles applications dépendent d’un composant en fin de vie ?
- existe-t-il un remplaçant standard ?
- quelle date de remédiation ?
- quel risque résiduel en cas de dérogation ?

## 2. Lifecycle dimensions

```text
Vendor lifecycle
Internal standard lifecycle
Platform lifecycle
Application dependency lifecycle
Contract/license lifecycle
```

Ces calendriers ne sont pas nécessairement alignés.

## 3. Vendor status vs internal status

Exemple :

```text
Vendor
Supported until 2028

Internal architecture
Deprecated for new workloads from 2026
```

Le produit reste supporté mais n’est plus recommandé.

## 4. Evidence management

Pour toute date importante :

- source ;
- URL/référence ;
- date de consultation ;
- niveau de confiance ;
- owner.

## 5. IT-Pedia

Le Store HOPEX publie un connecteur IT-Pedia permettant d’importer, aligner et mettre à jour les technologies du repository, ainsi que de suivre l’impact de changements d’obsolescence.

Cette intégration doit être distinguée des règles internes MayaBank de standards et de dette.

## 6. Technology health dimensions

Score pédagogique :

```text
Vendor support
Security exposure
Operational complexity
Skills availability
Architecture fit
Resilience fit
Cost efficiency
Automation maturity
```

## 7. Technology debt

Exemples :

- OS non supporté ;
- middleware ancien ;
- runtime non patchable ;
- scripts manuels critiques ;
- unique expert ;
- absence d’IaC ;
- protocole propriétaire ;
- dépendance réseau non redondée.

## 8. Debt item card

```text
Debt ID
Affected technology
Affected platforms/apps
Risk
Business impact
Workaround
Target state
Owner
Due date
Status
```

## 9. Obsolescence propagation

```text
Technology Product
→ Platform
→ Application
→ Process
→ Capability
→ Business Service
```

Cette chaîne permet de prioriser au-delà du seul âge technique.

## 10. Standards governance

Cycle :

```text
Proposed
→ Assessed
→ Approved/Preferred
→ Tolerated
→ Deprecated
→ Prohibited/Retired
```

## 11. Architecture exception

Une exception doit contenir :

- motivation ;
- scope ;
- risk acceptance ;
- compensating controls ;
- expiry ;
- remediation plan.

## 12. Technology Radar

Vue possible :

```text
Adopt
Trial
Assess
Hold
```

Le radar est une vue décisionnelle ; il ne remplace pas le catalogue canonique.

## 13. Skills risk

Une technologie peut être supportée mais devenir risquée si :

- compétences rares ;
- documentation faible ;
- communauté en déclin ;
- dépendance à un fournisseur unique.

## 14. License/contract risk

Analyser :

- metric de licence ;
- capacity limits ;
- renewal ;
- vendor support ;
- exit constraints.

## 15. Security vulnerability vs obsolescence

Une technologie récente peut être vulnérable ; une technologie ancienne peut être patchée mais proche de fin de support.

Les deux dimensions doivent rester distinctes.

## 16. MayaBank modernization triggers

```text
Legacy VM runtime EOL
Old Java version
Proprietary messaging dependency
Unsupported database release
Manual backup tooling
Single-site infrastructure
```

## 17. Prioritization

Combiner :

```text
Technical urgency
× business criticality
× dependency breadth
× remediation effort
× regulatory/security risk
```

## 18. Anti-patterns

- `old = obsolete` sans source ;
- `supported = strategic` ;
- dette sans owner ;
- exception permanente ;
- lifecycle vendor non daté ;
- remplacer une techno sans analyser les applications dépendantes.

## 19. Questions d’entretien

**Pourquoi IT-Pedia ne remplace-t-il pas la gouvernance interne ?**  
Il peut fournir des données technologiques et lifecycle, mais la décision Preferred/Deprecated et la trajectoire dépendent du contexte de l’entreprise.

**Pourquoi le blast radius compte-t-il dans l’obsolescence ?**  
Parce qu’une technologie peu répandue et une technologie utilisée par 200 applications n’ont pas la même priorité de transformation.
