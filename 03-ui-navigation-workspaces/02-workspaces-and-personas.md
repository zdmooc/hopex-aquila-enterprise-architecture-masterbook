# 02 — Home, Workspaces & Personas

## 1. Workspace : contexte de travail, pas nouvelle base

Un workspace sert à organiser l'expérience d'un profil ou d'un besoin. Il ne doit pas être compris comme un repository séparé.

Mental model :

```text
Repository commun
   ↓
Rights / Solution / Persona
   ↓
Workspace
   ↓
Tasks / Lists / Objects / Reports / Diagrams
```

Le contenu disponible dépend donc de la configuration réelle.

## 2. Personas typiques

Le Web Front-End HOPEX est officiellement destiné à plusieurs familles d'utilisateurs. Pour MayaBank, on retient les personas pédagogiques suivants.

### Enterprise Architect

Questions :

- quelles capabilities sont soutenues ?
- quelles applications sont stratégiques ?
- quels dépendances et impacts ?
- quelles transformations ?

### Solution Architect

Questions :

- quelles applications/services existent déjà ?
- quels standards technologiques ?
- quels systèmes impactés ?
- quelles intégrations ?

### Application Owner

Questions :

- ma fiche est-elle complète ?
- lifecycle correct ?
- owner et coûts renseignés ?
- dépendances applicatives correctes ?

### Process Owner

Questions :

- quels processus ?
- quels participants ?
- quelles applications supportent le processus ?

### Data / Information Architect

Questions :

- quels objets/domaines de données ?
- quelles applications produisent/consomment ?
- quelles classifications ?

### Risk / Control stakeholder

Questions :

- quels assets sont critiques ?
- quels risques et contrôles ?
- quels impacts en cas de changement ?

## 3. Concevoir un bon point d'entrée

Un bon workspace doit réduire le temps entre :

```text
Question
→ objet / liste / vue pertinente
→ décision
```

Il ne doit pas être une page décorative remplie de widgets non actionnables.

## 4. Structure recommandée d'un workspace MayaBank

### Architecture Board

```text
My reviews
Objects requiring decision
Applications without target lifecycle
Critical dependencies
Current transformation initiatives
Recent architecture changes
```

### Payments Architecture

```text
Payment capabilities
Payment processes
Payment applications
Integration landscape
Technology standards
Transformation roadmap
```

### Application Owner

```text
My applications
Data-quality alerts
Lifecycle decisions
Pending validations
Dependencies requiring review
```

Les intitulés ci-dessus sont des **patterns pédagogiques**, pas des noms d'écrans garantis par HOPEX.

## 5. Workspace vs dashboard

Un dashboard répond surtout à :

```text
What is the current state?
Where are the anomalies?
What deserves attention?
```

Un workspace répond plus largement à :

```text
What can I do from here?
```

## 6. Workspace vs security

Ne jamais supposer qu'un objet absent du workspace est inaccessible pour raison de sécurité.

Vérifier :

- filtres ;
- périmètre fonctionnel ;
- solution ;
- droits ;
- état de publication ;
- recherche globale ;
- configuration du workspace.

## 7. Navigation orientée tâche

Exemple : Architecture Board doit décider si `Legacy Payment Gateway` peut être retirée.

Mauvaise navigation :

```text
ouvrir 12 diagrammes au hasard
```

Meilleure navigation :

```text
Search Legacy Payment Gateway
→ canonical object
→ inbound/outbound relationships
→ supported processes/capabilities
→ consuming/consumed applications
→ technology dependencies
→ lifecycle / roadmap
→ decision
```

## 8. Mesures d'adoption

Un workspace utile peut être évalué avec :

- temps moyen pour trouver un objet ;
- proportion d'objets modifiés via flux gouverné ;
- taux de fiches complètes ;
- nombre de doublons créés ;
- taux de décisions avec traçabilité ;
- utilisateurs actifs par persona.

## 9. Anti-patterns

- un workspace identique pour tous ;
- 30 tuiles sans hiérarchie ;
- navigation basée sur l'organigramme uniquement ;
- widgets sans owner ;
- duplication de listes pour chaque équipe ;
- espace "mes applications" sans règle de responsabilité.

## 10. Exercice

Dessiner trois workspaces MayaBank :

1. Enterprise Architect ;
2. Application Owner ;
3. Architecture Board.

Pour chaque composant affiché, préciser :

```text
Question answered
Object type
Source
Action possible
Owner
```

Si un composant ne répond à aucune question, le retirer.