# 06 — Lifecycle, Obsolescence & Technical Debt

## 1. Le lifecycle comme donnée de décision

Un champ de lifecycle n'a de valeur que s'il déclenche une action.

```text
Technology deprecated
→ Applications impacted
→ Business capabilities exposed
→ Migration decision
→ Initiative / roadmap
```

La chaîne doit être interrogeable.

## 2. Trois lifecycles différents

### Lifecycle applicatif

```text
Invest / Maintain / Contain / Retire
```

### Lifecycle technologique interne

```text
Emerging / Preferred / Permitted / Deprecated / Forbidden
```

### Lifecycle fournisseur

```text
Release
Maintenance
End of standard support
Extended support
End of life
```

Ne pas fusionner ces trois concepts dans un seul statut.

## 3. Obsolescence

Une technologie est à risque si, par exemple :

- elle n'est plus supportée ;
- la version est trop ancienne ;
- les compétences disparaissent ;
- les correctifs de sécurité cessent ;
- le produit n'est plus stratégique ;
- le coût de maintien augmente ;
- elle bloque une transformation.

## 4. Santé technique d'une application

Score pédagogique :

| Dimension | Exemple |
|---|---|
| Runtime | Java 8 / obsolete |
| Framework | unsupported |
| Middleware | deprecated |
| Database | strategic / supported |
| OS | nearing EOL |
| Architecture | tightly coupled |
| Security | gaps |
| Operations | manual |

L'objectif n'est pas de fabriquer un score opaque, mais de conserver les faits qui expliquent la décision.

## 5. Date de fin de support

Pour chaque date :

- source ;
- version concernée ;
- date de dernière vérification ;
- owner ;
- interprétation interne.

Une date copiée sans source peut créer une fausse urgence.

## 6. Technology lifecycle content

Le positionnement public de HOPEX met en avant du contenu de lifecycle technologique intégré à l'offre et l'analyse des impacts business à travers applications et technologies.

Le masterbook retient donc comme use case prioritaire :

```text
Technology lifecycle
→ App usage
→ Business impact
```

## 7. Heatmap

Exemple :

```text
RED    = obsolete + critical dependency
ORANGE = support ending within horizon
YELLOW = non-standard
GREEN  = preferred / supported
```

La couleur doit être dérivée des données, pas peinte manuellement.

## 8. MayaBank — exemple WAS

Current :

```text
Legacy Payment Hub
→ WebSphere Application Server
→ old Java runtime
```

Target :

```text
Payment Orchestrator
→ OpenShift
→ Java current LTS
```

Le plan de migration doit être justifié par :

- risque support ;
- coût ;
- résilience ;
- time-to-market ;
- architecture target.

## 9. MayaBank — exemple Oracle/Exadata

Il ne faut pas conclure :

```text
Oracle = legacy donc retire
```

La décision dépend de :

- usage ;
- criticité ;
- version ;
- support ;
- coûts ;
- performance ;
- stratégie data ;
- alternatives.

Le repository doit permettre une décision argumentée.

## 10. Debt register

Un registre de dette peut relier :

```text
Debt Item
→ Technology
→ Application
→ Risk
→ Owner
→ Remediation initiative
→ Target date
```

La MetaClass exacte dépend de la solution/configuration ; c'est le pattern de gouvernance qui importe.

## 11. Priorisation

Priorité = combinaison de :

- business criticality ;
- end-of-support horizon ;
- security exposure ;
- number of dependent apps ;
- migration complexity ;
- transformation opportunity.

## 12. Anti-patterns

- lifecycle rempli une fois puis oublié ;
- aucune source de date ;
- toutes les technologies marquées `Strategic` ;
- score global sans faits ;
- obsolescence non reliée aux apps ;
- migration sans target standard ;
- technologie `Retired` toujours utilisée par 30 applications sans alerte.

## 13. Questions d'entretien

**Comment HOPEX aide-t-il sur l'obsolescence ?**  
En reliant le lifecycle des technologies au portefeuille applicatif et aux impacts métier.

**Pourquoi séparer vendor lifecycle et enterprise lifecycle ?**  
Parce qu'une technologie peut être supportée par l'éditeur mais déjà non stratégique dans l'entreprise.

**Que faire d'une dette détectée ?**  
La relier à un owner, un risque et une action de transformation avec horizon.
