# 01 — UI Baseline & Working Principles

## 1. Baseline produit

La Partie III vise **HOPEX Aquila 6.2**, Web Front-End `hopex.dtpx`, branche documentaire **62.18.x**. Au 8 septembre 2026, le Store MEGA affiche `62.18.0+143`, publié le 2 septembre 2026.

Le Store décrit le Web Front-End comme le portail web destiné notamment aux enterprise architects, process modelers, risk managers, auditors et autres stakeholders EA/GRC.

Cette partie documente donc les **principes d'usage stables**. Les noms exacts de menus, boutons, panneaux ou tuiles peuvent varier selon :

- la solution HOPEX installée ;
- les droits ;
- la configuration du client ;
- la version de la release ;
- les personnalisations ;
- le rôle courant.

## 2. Ne pas apprendre l'interface comme une suite de clics

Une mauvaise formation HOPEX ressemble à :

```text
Menu X → bouton Y → onglet Z → bouton Save
```

Ce savoir devient fragile dès qu'un écran change.

Un architecte doit plutôt comprendre :

```text
Persona
→ Workspace
→ Search / Navigation
→ Canonical Object
→ Properties
→ Relationships
→ Views / Lists / Diagrams
→ Analysis
→ Governance action
```

## 3. L'interface est une projection du repository

Principe central :

```text
UI ≠ repository
UI = projection du repository adaptée à un usage
```

Une fiche Application ne crée pas une nouvelle vérité. Elle expose une instance, ses attributs et ses associations.

Une liste n'est pas un inventaire indépendant. Elle est une vue tabulaire d'objets existants.

Un diagramme n'est pas un fichier autonome. Il doit réutiliser les objets canoniques lorsque la solution et le modèle le prévoient.

## 4. Les cinq gestes d'un utilisateur mature

1. **chercher avant de créer** ;
2. **ouvrir l'objet canonique** ;
3. **lire les propriétés avant de modifier** ;
4. **naviguer par relations** ;
5. **utiliser listes/diagrammes/rapports comme vues complémentaires**.

## 5. Lecture en couches

Sur toute fiche HOPEX, raisonner selon :

```text
IDENTITY
Qui est cet objet ?

CLASSIFICATION
Quel type / domaine / catégorie ?

OWNERSHIP
Qui en répond ?

LIFECYCLE
Quel état et quelle trajectoire ?

RELATIONSHIPS
À quoi est-il relié ?

EVIDENCE
Quelle source / quelle date de revue ?
```

## 6. Rôle des droits

Deux utilisateurs peuvent voir des expériences différentes parce que leurs droits diffèrent.

Ne pas conclure :

```text
"La fonctionnalité n'existe pas"
```

avant de vérifier :

```text
solution activée ?
licence ?
profil ?
droit lecture ?
droit édition ?
workspace ?
configuration ?
```

## 7. MayaBank — règle de navigation

Pour tout objet, on doit pouvoir répondre à trois questions :

```text
WHY does it exist?
WHAT does it support/use?
WHAT changes if it disappears?
```

Exemple : `Payment Orchestrator`.

```text
Why    → instant payment capability/process
Uses   → fraud, event streaming, data platform
Impact → payment initiation degraded/unavailable
```

## 8. Pièges

- créer un objet parce qu'on ne le retrouve pas en 20 secondes ;
- utiliser un diagramme comme inventaire maître ;
- modifier un attribut sans connaître sa source ;
- confondre absence d'affichage et absence de donnée ;
- confondre workspace et périmètre de sécurité ;
- apprendre une capture écran comme vérité durable.

## 9. Réflexe entretien

**Question : comment vous formez un architecte à HOPEX ?**

Réponse attendue : je lui apprends d'abord le repository, le métamodèle, les objets canoniques et la navigation par relations. Les clics viennent ensuite.