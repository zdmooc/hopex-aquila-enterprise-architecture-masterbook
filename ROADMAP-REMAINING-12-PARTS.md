# Roadmap de reprise — Parties XIII à XXIV

## État du masterbook

- Programme total : **24 parties**.
- Parties terminées : **I à XII**.
- Avancement : **12 / 24 = 50 %**.
- Prochaine partie à construire : **Partie XIII — IT Business Management & Application Portfolio**.
- Dernier commit fonctionnel avant ce fichier de reprise : `30fbab452c00dc19a444233aead9d1ca680372eb`.

Ce document est le **point de reprise officiel** pour terminer le masterbook ultérieurement.

---

# Parties restantes

## Partie XIII — IT Business Management & Application Portfolio

Objectif : transformer le catalogue applicatif en portefeuille pilotable.

À couvrir au minimum :

- Application Portfolio Management ;
- application inventory et ownership ;
- business fit / technical fit ;
- functional redundancy ;
- lifecycle et obsolescence ;
- cost/value/risk dimensions ;
- TIME / 6R ou cadres équivalents comme méthodes, sans les attribuer à Hopex si non vérifiés ;
- rationalisation ;
- decommissioning ;
- SaaS/COTS/custom/legacy ;
- portfolio heatmaps ;
- MayaBank Application Portfolio ;
- labs, questions corrigées et sources officielles.

## Partie XIV — IT Portfolio Management & Transformation Roadmaps

Objectif : relier l’existant, les cibles et les initiatives de transformation.

À couvrir :

- initiatives / projects / programs ;
- current / transition / target ;
- capability gaps ;
- application and technology roadmaps ;
- dependencies entre initiatives ;
- sequencing ;
- transition architectures ;
- migration waves ;
- portfolio prioritization ;
- risk/value/cost dependencies ;
- roadmap governance ;
- MayaBank transformation roadmap.

## Partie XV — Reports, Dashboards, Analysis & Decision Support

Objectif : exploiter le repository pour la décision.

À couvrir :

- lists, reports, dashboards ;
- KPIs et indicators ;
- heatmaps ;
- portfolio analytics ;
- impact analysis outputs ;
- executive reporting ;
- Architecture Board packs ;
- Hopex 360 / publication quand vérifié ;
- data freshness et confiance ;
- dashboard anti-patterns ;
- MayaBank decision cockpit.

## Partie XVI — Repository Governance & Data Quality

Objectif : rendre le repository durable et fiable.

À couvrir :

- governance operating model ;
- object ownership ;
- stewardship ;
- canonical records ;
- completeness / accuracy / freshness ;
- duplicate detection ;
- naming rules ;
- relationship quality ;
- source authority ;
- evidence dates ;
- review campaigns ;
- quality KPIs ;
- remediation workflow ;
- MayaBank repository governance.

## Partie XVII — Administration, Roles, Rights & Security

Objectif : comprendre la gouvernance opérationnelle de la plateforme.

À couvrir uniquement sur base vérifiée :

- users ;
- personas ;
- profiles ;
- permissions ;
- access control ;
- workspace access ;
- administration boundaries ;
- authentication / SSO si documenté publiquement ;
- least privilege ;
- separation of duties ;
- auditability ;
- MayaBank role model.

## Partie XVIII — Customization, Extensions & Metamodel Governance

Objectif : étendre Hopex sans détruire le modèle standard.

À couvrir :

- standard vs custom metamodel ;
- MetaStudio ;
- MetaClass / MetaAttribute / MetaAssociation extensions ;
- naming conventions ;
- extension decision framework ;
- upgrade impact ;
- technical debt de customisation ;
- governance board ;
- extension lifecycle ;
- anti-patterns ;
- MayaBank extension cases.

## Partie XIX — Import, Export & Data Exchange

Objectif : industrialiser les échanges de données.

À couvrir après vérification des fonctions Aquila actuelles :

- Excel import/export ;
- templates officiels ;
- bulk updates ;
- CSV/Excel boundaries ;
- import keys ;
- deduplication ;
- referential integrity ;
- data validation ;
- reconciliation ;
- source-of-truth rules ;
- incremental loads ;
- error handling ;
- MayaBank onboarding datasets.

## Partie XX — REST, GraphQL, ServiceNow, MCP & AI Integrations

Objectif : connecter Hopex à l’écosystème SI.

À couvrir avec vérification web systématique au moment de la reprise :

- REST API ;
- GraphQL ;
- MetaModel API ;
- endpoint patterns officiellement documentés ;
- ServiceNow integration ;
- MCP Server officiel ;
- authentication/authorization des APIs si public ;
- integration patterns ;
- synchronization ownership ;
- conflict resolution ;
- CMDB ↔ EAM boundary ;
- AI use cases sans inventer de fonctions ;
- MayaBank integration architecture.

## Partie XXI — MayaBank Complete HOPEX Enterprise Model

Objectif : assembler toutes les parties dans un seul modèle cohérent.

À produire :

- business architecture ;
- capabilities ;
- processes ;
- applications ;
- information/data ;
- technology/platforms ;
- risks/controls ;
- organizations/owners ;
- initiatives ;
- current/target ;
- dependencies ;
- matrices ;
- views ;
- portfolio ;
- governance ;
- naming/IDs ;
- cross-layer traceability de bout en bout.

Le modèle final ne doit pas réinventer les objets déjà définis dans les Parties V à XII.

## Partie XXII — Hands-on Labs, Interview Cases & Operational Playbook

Objectif : rendre le masterbook directement exploitable pour missions et entretiens.

À produire :

- labs consolidés ;
- scénarios guidés ;
- architecture review exercises ;
- data quality exercises ;
- impact-analysis exercises ;
- rationalization exercises ;
- API/integration exercises ;
- Architecture Board cases ;
- mission 30/60/90 days ;
- interview cases architecte solution / enterprise architect / Hopex.

## Partie XXIII — English, Glossary & Question Bank

Objectif : consolider le vocabulaire professionnel et la préparation entretien.

À produire :

- glossary FR/EN ;
- concepts Hopex ;
- TOGAF/ArchiMate/Hopex distinctions ;
- technical vocabulary ;
- application portfolio vocabulary ;
- data/technology vocabulary ;
- phrases d’entretien ;
- questions courtes ;
- questions avancées ;
- réponses corrigées ;
- pièges fréquents.

## Partie XXIV — Official Sources, Training/Certification Mapping & Final Audit

Objectif : fermer le masterbook proprement et vérifier l’ensemble.

À réaliser impérativement :

- revérifier la baseline Aquila courante au moment de la reprise ;
- revérifier Core/Web/REST/GraphQL/MCP/ServiceNow ;
- auditer tous les liens officiels ;
- distinguer fait produit / best practice / hypothèse MayaBank ;
- supprimer toute affirmation non vérifiée ;
- vérifier les frontières HOPEX / TOGAF / ArchiMate / CMDB / BPM runtime ;
- vérifier cohérence des noms MayaBank ;
- vérifier liens internes du dépôt ;
- vérifier doublons de contenu ;
- construire un index final ;
- établir le mapping formations/certifications disponibles publiquement ;
- produire la checklist finale de préparation mission/entretien.

---

# Règles de reprise

À la reprise, suivre cet ordre :

1. lire le `README.md` racine ;
2. lire ce fichier ;
3. vérifier le HEAD de `main` ;
4. relire la Partie XII pour conserver la continuité ;
5. commencer directement par la Partie XIII ;
6. revérifier sur le Web les faits produit susceptibles d’avoir évolué ;
7. conserver la distinction : **fait produit vérifié / pratique d’architecture / hypothèse MayaBank** ;
8. ne jamais inventer le comportement du métamodèle ou des écrans Hopex ;
9. ne pas recopier de documentation ou de formation propriétaire ;
10. construire chaque partie avec contenu substantiel, MayaBank, anti-patterns, labs, questions corrigées et sources ;
11. produire **un seul commit propre par partie** ;
12. vérifier après chaque partie : `ahead_by=1`, `behind_by=0`, `total_commits=1` par rapport au commit propre précédent ;
13. vérifier que `main` pointe sur le commit final ;
14. mettre à jour le README racine après chaque partie.

---

# Règles conceptuelles à conserver jusqu’à la fin

```text
TOGAF = méthode et gouvernance
ArchiMate = langage de modélisation
HOPEX = plateforme EAM / repository / analyse / gouvernance / portfolio / transformation

HOPEX object ≠ automatiquement ArchiMate element
HOPEX diagram ≠ automatiquement ArchiMate viewpoint normatif
Capability ≠ Process
Application ≠ Technology
EAM repository ≠ CMDB
HOPEX ≠ runtime BPM engine
Current architecture ≠ Target architecture
Target architecture ≠ Migration plan
```

---

# Commande de reprise

Quand le travail reprend :

```text
SUIVANT
```

signifie :

> construire complètement la prochaine partie non terminée, sans redemander d’autorisation.

Le prochain `SUIVANT` doit donc démarrer par :

**Partie XIII — IT Business Management & Application Portfolio**.
