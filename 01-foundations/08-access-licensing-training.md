# 08 — Accès, licences, training et environnement

## 1. Produit propriétaire

HOPEX est une plateforme propriétaire MEGA International. Contrairement à ArchiMate, on ne peut pas supposer qu'un lecteur dispose librement d'une instance complète à installer.

Le masterbook sépare donc :

```text
Knowledge lab
→ réalisable sans instance HOPEX

Repository simulation
→ réalisable avec Markdown/CSV/JSON

Product lab
→ nécessite accès/licence/environnement HOPEX
```

## 2. Store officiel

Le Store MEGA publie les composants et add-ons. Plusieurs modules affichent explicitement :

```text
Sign in to download the module
```

L'existence d'une fiche Store ne signifie donc pas que le module est librement installable par n'importe quel utilisateur.

## 3. Licences fonctionnelles

Pour les APIs, la documentation Store indique que l'accès aux données d'une solution peut dépendre des licences fonctionnelles correspondantes.

Conséquence :

```text
API installed
≠ access to every HOPEX solution
```

Avant un POC d'intégration, valider :

- licence ;
- schema disponible ;
- authentification ;
- droits utilisateur ;
- objets accessibles ;
- mutations autorisées.

## 4. Training database

Une sauvegarde officielle de training Aquila 6.2 CU5 est publiée avec des données de cours et un prérequis SQL Server 2022.

Cours listés :

- IT Business Management ;
- IT Portfolio Management ;
- Business Process Analysis ;
- IT Architecture ;
- Information Architecture ;
- Data Governance ;
- Integrated Risk Management.

Cette ressource est particulièrement pertinente si un environnement HOPEX correspondant est obtenu légalement.

## 5. Demo database

Le Store publie aussi des backups Demo Aquila 6.2 contenant des données, rapports et utilisateurs destinés à démonstration/test.

Règle :

```text
Demo data = support d'apprentissage
not production reference architecture
```

## 6. Environnement de lab cible

Si un accès officiel est obtenu, le masterbook cherchera à documenter :

```text
HOPEX Aquila 6.2
+ compatible Core/Web
+ SQL Server compatible
+ training/demo DB autorisée
+ user architect
+ user admin si nécessaire
+ GraphQL/REST add-ons si disponibles
```

Nous ne promettons pas un déploiement Docker/OpenShift non documenté par l'éditeur.

## 7. Ce que nous pouvons apprendre sans licence

Beaucoup de compétences d'architecte HOPEX ne nécessitent pas d'instance au départ :

- repository design ;
- object identity ;
- naming ;
- ownership ;
- lifecycle ;
- source-of-truth ;
- application portfolio ;
- dependency modeling ;
- architecture governance ;
- mapping ServiceNow ;
- API query design ;
- data quality ;
- roadmap design ;
- interview scenarios.

## 8. Simulateur MayaBank

Avant l'accès produit, nous construirons des datasets pédagogiques :

```text
applications.csv
capabilities.csv
processes.csv
technologies.csv
relationships.csv
owners.csv
lifecycles.csv
```

Puis des contrôles automatiques pourront détecter :

- duplicate IDs ;
- orphan objects ;
- missing owners ;
- invalid lifecycle ;
- unresolved relationships ;
- stale review dates.

Ces fichiers ne prétendront pas être un format d'import HOPEX tant que ce format n'aura pas été vérifié.

## 9. Stratégie d'apprentissage à deux vitesses

### Track A — sans instance

```text
concepts
→ repository governance
→ MayaBank dataset
→ mapping exercises
→ API reasoning
→ interview cases
```

### Track B — avec instance

```text
create object
→ edit properties
→ create relationships
→ diagrams/matrices
→ reports
→ API queries
→ integrations
→ governance workflows
```

## 10. Demande d'accès à préparer

Lorsqu'on contacte MEGA/partenaire/entreprise, demander précisément :

- trial ou sandbox disponible ?
- version Aquila ?
- solutions incluses ?
- durée ?
- droit d'utiliser training DB ?
- accès API ?
- documentation ?
- restrictions de publication de captures ?

## 11. Sécurité et secrets

Aucun repository GitHub public ne doit contenir :

- mot de passe d'environnement ;
- token HOPEX ;
- bearer token ;
- URL interne privée ;
- export client confidentiel ;
- backup de repository propriétaire ;
- données réelles d'entreprise.

Même si un mot de passe apparaît publiquement sur une fiche de training officielle, le masterbook évitera de le recopier comme secret opérationnel.

## 12. Critère de réussite

Le manque d'instance ne doit pas bloquer l'apprentissage de l'architecture EAM. Il limite seulement les labs spécifiques à l'UI et aux APIs réelles.
