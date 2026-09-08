# 01 — HOPEX IT Architecture : rôle et méthode

## 1. Finalité

HOPEX IT Architecture doit permettre à l’architecte de répondre à des questions concrètes sur le SI :

- quelles applications supportent un domaine métier ou une capacité ?
- quelles applications échangent entre elles ?
- quelles technologies supportent ces applications ?
- quels composants arrivent en fin de vie ?
- quels environnements ou déploiements sont critiques ?
- quelles dépendances rendent une transformation risquée ?
- quelle architecture cible réduit la dette et le couplage ?

La valeur ne vient donc pas d’un diagramme isolé, mais du lien entre **objets canoniques, propriétés, relations, vues et analyses**.

## 2. Ce que confirme le positionnement officiel

Les pages publiques de Bizzdesign/MEGA mettent en avant la capacité de HOPEX à connecter dans un référentiel commun :

- applications ;
- business capabilities ;
- processus ;
- data flows et interdépendances ;
- investissements technologiques ;
- analyses d’impact ;
- rationalisation et cloud migration.

Le présent chapitre exploite ces axes comme structure pédagogique.

## 3. La chaîne IT Architecture

```text
Business Capability / Process
        ↓
Application
        ↓
Application Service / Interface / Flow
        ↓
Technology / Platform / Software Technology
        ↓
Deployment / Environment
        ↓
Infrastructure / Runtime
        ↓
Lifecycle / Standard / Risk
        ↓
Current → Transition → Target
```

Cette chaîne est logique. Les noms exacts d’objets disponibles dans une instance HOPEX dépendent des solutions activées et du métamodèle.

## 4. Les quatre niveaux à ne pas confondre

### Architecture métier
Pourquoi le SI existe-t-il et que supporte-t-il ?

### Architecture applicative
Quelles applications et interactions réalisent le comportement attendu ?

### Architecture technologique
Quelles technologies, plateformes et standards supportent les applications ?

### Architecture de déploiement
Où et comment les solutions sont-elles instanciées dans des environnements concrets ?

Une architecture qui mélange les quatre niveaux dans un seul objet devient difficile à analyser.

## 5. Application logique vs runtime

Exemple MayaBank :

```text
Application logique
MayaBank Payment Orchestrator

Runtime possible
- namespace payments-prod
- deployment payment-orchestrator-v42
- 6 pods
- cluster OCP-PROD-A
```

Le repository EAM doit privilégier le niveau stable nécessaire aux décisions. Les détails très volatils restent généralement mieux gérés dans une CMDB, un outil de plateforme ou d’observabilité.

## 6. Architecture current / target

Le travail d’architecture ne consiste pas uniquement à documenter l’existant.

```text
CURRENT
legacy integration
point-to-point flows
obsolete middleware
manual failover

TARGET
event-driven integration
API-managed access
container platform
standardized observability
```

HOPEX doit permettre de relier les états, les objets concernés et les décisions de transformation.

## 7. Qualité d’un modèle IT Architecture

Un modèle exploitable possède :

- des objets uniques ;
- un périmètre explicite ;
- des relations sémantiques ;
- des owners ;
- un lifecycle ;
- des technologies qualifiées ;
- des dépendances vérifiables ;
- une source ;
- des vues adaptées aux questions ;
- une distinction current/target.

## 8. Anti-pattern : architecture par dessins

Mauvais :

```text
PowerPoint A : App X → App Y
Diagramme HOPEX B : App X → App Z
Excel C : App X dépend de Middleware M
```

Meilleur :

```text
App X = objet canonique
Relations = repository
Diagrammes = projections du graphe
Rapports = requêtes sur le même graphe
```

## 9. Anti-pattern : tout mettre dans HOPEX

Le but n’est pas de créer une CMDB bis.

Ne pas modéliser automatiquement :

- chaque pod ;
- chaque VM éphémère ;
- chaque endpoint observé ;
- chaque instance de base ;
- chaque release mineure.

Ne les inclure que si une décision d’architecture le justifie.

## 10. Cycle de travail recommandé

```text
1. définir le concern
2. identifier les objets canoniques
3. vérifier le current
4. compléter relations critiques
5. qualifier lifecycle/standards
6. produire la vue utile
7. analyser impacts
8. définir target
9. rattacher transformation
10. faire valider
```

## 11. Questions d’entretien

**À quoi sert HOPEX IT Architecture ?**  
À maintenir une représentation gouvernée des applications, technologies, dépendances et transformations afin d’analyser le SI et de prendre des décisions d’architecture.

**Quelle différence avec une CMDB ?**  
La CMDB vise le run et les configurations opérationnelles ; l’EAM vise les dépendances structurantes, les choix, les standards et la transformation.

**Quelle première erreur éviter ?**  
Créer les diagrammes avant de gouverner les objets et les relations.
