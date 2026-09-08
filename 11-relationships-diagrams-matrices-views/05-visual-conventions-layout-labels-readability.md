# 05 — Visual Conventions, Layout, Labels & Readability

## 1. Une vue lisible est une architecture plus facile à gouverner

La mise en page ne change pas la sémantique, mais elle change fortement la compréhension.

Un diagramme doit permettre au lecteur d’identifier rapidement :

- le sujet ;
- le sens de lecture ;
- les groupes ;
- les dépendances majeures ;
- les exceptions ;
- la temporalité ;
- la légende.

## 2. Sens de lecture

Choisir une convention principale.

Exemples :

```text
left → right : value / process / flow
up → down    : business → application → technology
inside → outside : decomposition
```

Éviter les diagrammes où chaque zone suit une direction différente.

## 3. Alignment

Aligner :

- objets de même niveau ;
- étapes d’un flux ;
- éléments d’une même couche ;
- objets d’un même lifecycle si le layout le permet.

## 4. Grouping

Grouper selon une dimension explicitée :

```text
Business domain
Application domain
Security zone
Deployment site
Lifecycle
Transformation wave
```

Ne pas changer de critère de grouping au milieu de la vue.

## 5. Containers

Les conteneurs graphiques doivent correspondre à un concept réel ou à une convention documentée.

Exemple :

```text
Payments Domain
contains visual representations of payment applications
```

Ne pas laisser croire qu’un conteneur graphique implique une composition du métamodèle si ce n’est pas le cas.

## 6. Color

La couleur peut représenter :

- lifecycle ;
- health ;
- criticality ;
- maturity ;
- ownership ;
- transformation status.

Mais une couleur doit avoir :

- une légende ;
- une seule sémantique par vue ;
- un contraste accessible.

## 7. Ne pas dépendre uniquement de la couleur

Prévoir également :

- label ;
- iconographie ;
- pattern ;
- annotation ;
- grouping.

Exemple : `Deprecated` doit être lisible même en impression noir et blanc.

## 8. Shapes

Ne pas attribuer arbitrairement une forme différente à chaque objet.

Préférer :

```text
same metaclass / concept family
→ same basic visual grammar
```

## 9. Lines

Conventions possibles :

```text
solid      = active relation
dashed     = target/planned relation
thick      = critical path
```

Ces conventions sont pédagogiques ; ne pas les présenter comme standards HOPEX natifs.

## 10. Arrowheads

Une flèche doit renforcer le sens sémantique.

Exemple :

```text
Producer → Consumer
Current → Target
Parent → Child
```

Éviter les flèches bidirectionnelles par défaut.

## 11. Labels

Un lien important doit avoir un libellé utile lorsque le sens n’est pas évident.

Mauvais :

```text
A → B
```

Meilleur :

```text
Payment Orchestrator → publishes → PaymentStatusChanged
```

## 12. Abbreviations

Les acronymes doivent être connus ou légendés.

Mauvais :

```text
PO → FDS → CAG → ES
```

sans légende.

## 13. Crossing lines

Réduire les croisements par :

- regroupement ;
- orientation ;
- duplication uniquement de représentation si la plateforme le permet sans dupliquer l’objet ;
- vues secondaires ;
- decomposition.

## 14. Density

Règle pratique : si le lecteur doit zoomer et chercher plusieurs minutes pour comprendre le sujet, la vue doit probablement être découpée.

## 15. White space

L’espace vide est utile pour :

- séparer des domaines ;
- montrer des boundaries ;
- améliorer la lecture.

Ne pas remplir chaque zone disponible.

## 16. Titles

Un titre utile précise :

```text
MayaBank — Instant Payment Application Cooperation — Current — PROD — 2026-Q3
```

Plutôt que :

```text
Architecture Diagram 12
```

## 17. Legend

La légende doit expliquer :

- couleurs ;
- types de lignes ;
- horizons ;
- statuts ;
- symboles non standard.

## 18. Annotations

Utiliser avec parcimonie pour :

- hypothèse ;
- décision ;
- exception ;
- source ;
- date.

Un commentaire important pour l’analyse devrait devenir un objet ou une propriété gouvernée si nécessaire.

## 19. Current / target

Trois patterns :

### Separate views
Current et Target dans deux vues.

### Side-by-side
Deux panneaux comparables.

### Overlay
Même vue avec statuts explicites.

Le choix dépend de la complexité.

## 20. MayaBank — visual grammar

Convention pédagogique :

```text
Top row    : Capability / Process
Middle     : Applications
Lower      : Platforms / Technologies
Side lane  : Risks / Initiatives
```

Les relations critiques sont limitées aux liens nécessaires à la décision.

## 21. Accessibility

Vérifier :

- taille de texte ;
- contraste ;
- impression/PDF ;
- distinction des statuts sans couleur ;
- terminologie claire.

## 22. Review checklist

1. Titre explicite ?
2. Scope visible ?
3. Sens de lecture ?
4. Couleur légendée ?
5. Pas de sémantique uniquement par couleur ?
6. Relations lisibles ?
7. Croisements raisonnables ?
8. Temporalité visible ?
9. Acronymes compris ?
10. Vue encore lisible exportée ?

## 23. Anti-patterns

- rainbow architecture ;
- cinq sens de lecture ;
- police minuscule ;
- flèche pour tout ;
- légende absente ;
- code couleur différent entre vues du même portfolio ;
- décoration qui ressemble à une sémantique ;
- vue conçue seulement pour un écran 4K.

## 24. Questions d’entretien

**Pourquoi la couleur ne suffit-elle pas ?**  
Pour l’accessibilité, l’impression et pour éviter qu’une sémantique critique disparaisse hors contexte.

**Pourquoi standardiser les conventions ?**  
Pour réduire le temps d’interprétation et faciliter la comparaison entre domaines et projets.

**La mise en page doit-elle modifier le repository ?**  
Non. Elle organise la représentation, pas la vérité sémantique.