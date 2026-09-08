# 09 — Collaboration, Validation & Workflows

## 1. Pourquoi la collaboration est une fonction d’architecture

Un repository EAM n’est pas un espace de saisie individuel. Sa valeur vient de la capacité à faire contribuer plusieurs populations sans perdre la cohérence du référentiel.

Dans MayaBank :

```text
Architecte domaine Paiements
→ décrit l’application et ses dépendances

Owner métier
→ valide le rôle métier et la criticité

Platform Engineering
→ confirme les technologies supportées

CISO
→ ajoute exigences, risques et contrôles

Architecture Board
→ arbitre la cible et le lifecycle
```

Le point important est la séparation entre **contribution**, **validation** et **publication**.

## 2. Collaboration ≠ droits d’écriture partout

Une mauvaise gouvernance consiste à donner le droit de modifier n’importe quel objet à toute personne qui participe à un programme.

Une meilleure approche distingue :

- consultation ;
- contribution sur un périmètre ;
- validation ;
- administration ;
- publication ;
- intégration automatique.

La configuration exacte dépend des rôles et licences HOPEX installés.

## 3. Cycle de vie d’une donnée d’architecture

Modèle recommandé :

```text
Draft
→ Reviewed
→ Approved
→ Published
→ Revalidated
→ Deprecated / Retired
```

Ce cycle n’est pas forcément un workflow produit standard identique chez tous les clients. C’est une pratique de gouvernance à adapter au mécanisme HOPEX disponible.

## 4. Comment traiter un changement

Exemple : changement de technologie du Payment Orchestrator.

```text
Current: Java 11 / WebSphere
Target : Java 21 / OpenShift
```

Ne pas simplement écraser l’information si la décision de transformation doit rester traçable.

Il faut pouvoir distinguer :

- information actuelle ;
- cible ;
- décision ;
- projet ou initiative ;
- date d’effet ;
- impacts ;
- responsable.

## 5. Review efficace

Une review doit répondre à des questions précises :

1. l’objet est-il canonique ?
2. l’owner est-il correct ?
3. le lifecycle est-il cohérent ?
4. les relations critiques sont-elles présentes ?
5. les technologies déclarées sont-elles pertinentes au niveau EA ?
6. existe-t-il des doublons ?
7. la source de l’information est-elle connue ?
8. la date de revue est-elle acceptable ?
9. la donnée sera-t-elle exploitable dans rapports et roadmaps ?
10. la modification casse-t-elle une intégration ?

## 6. Commentaires et échanges

Les capacités exactes de commentaires, tâches, notifications ou workflows varient selon les solutions HOPEX et leur configuration.

Le principe de masterbook est donc :

```text
ne pas documenter un bouton comme vérité universelle
mais documenter la responsabilité de collaboration
```

## 7. Workflow de validation MayaBank

Pour une nouvelle application logique :

```text
Architect creates draft
        ↓
Domain architect reviews semantics
        ↓
Application owner validates ownership/lifecycle
        ↓
Platform architect validates major technologies
        ↓
EA governance checks duplication and naming
        ↓
Published in repository
```

## 8. Workflow de décommissionnement

```text
Candidate for retirement
→ validate business dependencies
→ validate interfaces and data dependencies
→ identify replacement
→ link transformation initiative
→ set planned retirement date
→ monitor residual consumers
→ mark retired
→ archive/delete only if policy allows
```

La suppression physique immédiate est rarement la meilleure première action.

## 9. Collaboration et intégrations

Une donnée synchronisée automatiquement doit aussi avoir un processus de gouvernance.

Exemple : ServiceNow fournit une donnée technique.

```text
ServiceNow = source
HOPEX = consumer
```

Mais il faut encore définir :

- mapping ;
- fréquence ;
- conflit ;
- suppression ;
- ownership ;
- erreur de synchronisation ;
- audit.

## 10. Architecture Board

HOPEX peut soutenir un Architecture Board en fournissant :

- inventaire ;
- impacts ;
- dépendances ;
- roadmaps ;
- lifecycle ;
- rapports ;
- vues de décision.

Mais l’outil ne remplace pas la décision de gouvernance.

## 11. Anti-patterns

- tout le monde peut tout éditer ;
- aucun owner ;
- aucun statut de validation ;
- commentaires utilisés comme unique source de décision ;
- décision d’architecture non reliée aux objets impactés ;
- changement de lifecycle sans date ni justification ;
- synchronisation automatique qui écrase les choix EA ;
- suppression d’un objet sans impact analysis.

## 12. Questions d’entretien

**Pourquoi séparer contributeur et approbateur ?**  
Pour éviter qu’une personne qui fournit l’information soit aussi la seule à valider sa qualité et sa conformité.

**Un workflow résout-il la qualité du repository ?**  
Non. Un workflow structure le processus ; la qualité dépend aussi du métamodèle, des règles, des owners et des contrôles.

**Que faire si une source externe contredit HOPEX ?**  
Appliquer la règle de source autoritative par attribut ou domaine, plutôt qu’un écrasement arbitraire.
