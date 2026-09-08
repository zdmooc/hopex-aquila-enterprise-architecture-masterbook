# 11 — UI Governance & Anti-Patterns

## 1. L’interface peut masquer un problème de gouvernance

Une UI fluide ne garantit pas un repository sain.

On peut avoir :

- des pages objets bien remplies ;
- de beaux diagrammes ;
- des listes nombreuses ;

et malgré tout :

- doublons ;
- mauvais owners ;
- relations incohérentes ;
- données obsolètes ;
- statuts contradictoires.

La qualité se juge sur la cohérence du repository, pas sur l’esthétique de l’écran.

## 2. Anti-pattern — créer depuis le diagramme sans rechercher

Symptôme :

```text
Payment API
Payment API New
Payment_API
Payments API
```

Correction :

```text
Search
→ identify canonical object
→ reuse
→ create only if absent
```

## 3. Anti-pattern — utiliser une vue comme source de vérité

Un diagramme est une représentation partielle.

Erreur : conclure qu’un objet n’existe pas parce qu’il n’est pas dans la vue ouverte.

Réflexe :

```text
view
→ object page
→ repository search
→ related objects
```

## 4. Anti-pattern — propriétés libres pour des données structurantes

Exemple :

```text
Criticality = critique
Criticality = C1
Criticality = high
Criticality = very high
```

Si la donnée pilote des analyses, préférer une classification gouvernée.

## 5. Anti-pattern — description utilisée comme base de données

Une description narrative est utile pour le contexte.

Elle ne doit pas remplacer :

- owner ;
- lifecycle ;
- technology ;
- interfaces ;
- relations ;
- date de revue.

## 6. Anti-pattern — filtres personnels non reproductibles

Un architecte construit une vue utile mais personne ne sait la reproduire.

Pour les analyses importantes, documenter :

- population ;
- critères ;
- filtres ;
- exclusions ;
- date ;
- owner de l’analyse.

## 7. Anti-pattern — bulk edit sans contrôle

Les opérations de masse peuvent dégrader rapidement un référentiel.

Avant une mise à jour en volume :

1. définir la règle ;
2. exporter/contrôler le périmètre ;
3. tester sur sandbox ;
4. mesurer l’impact ;
5. appliquer ;
6. contrôler le résultat.

## 8. Anti-pattern — favoris utilisés comme taxonomie

Les favoris sont pratiques pour l’utilisateur mais ne remplacent pas :

- domaines ;
- classifications ;
- workspaces ;
- portfolios ;
- responsabilités.

## 9. Anti-pattern — diagrammes monstres

Un diagramme avec 200 objets mélange :

- inventaire ;
- architecture ;
- impact analysis ;
- roadmap ;
- gouvernance.

Créer plusieurs vues par concern.

## 10. Anti-pattern — workflow décoratif

Un workflow qui ne bloque rien, ne clarifie aucune responsabilité et ne laisse aucune trace ne crée pas de gouvernance réelle.

## 11. Anti-pattern — personnaliser l’UI avant le modèle

Avant d’ajouter des écrans ou champs :

```text
business need
→ metamodel check
→ governance rule
→ data source
→ UI need
```

Pas l’inverse.

## 12. Anti-pattern — tout exposer à tous

La visibilité doit correspondre au rôle et à l’usage.

Un stakeholder métier n’a pas besoin du même workspace qu’un administrateur du métamodèle.

## 13. Anti-pattern — copier la CMDB dans les écrans HOPEX

Si l’utilisateur voit 20 000 CIs volatils dans son workspace EA, le signal architectural disparaît.

Synchroniser et afficher uniquement les données utiles à la décision.

## 14. Anti-pattern — aucune date de fraîcheur

Un repository sans date de revue ne permet pas de distinguer vérité actuelle et donnée historique.

Métriques utiles :

- last review date ;
- last modified ;
- stale > 6/12/18 mois ;
- owner missing ;
- source missing.

## 15. Checklist de qualité UI

- [ ] chercher avant création ;
- [ ] ouvrir l’objet canonique ;
- [ ] renseigner uniquement les propriétés pertinentes ;
- [ ] privilégier les relations structurées ;
- [ ] distinguer current et target ;
- [ ] utiliser les listes pour les contrôles ;
- [ ] garder les diagrammes orientés concern ;
- [ ] documenter les filtres importants ;
- [ ] limiter les modifications de masse ;
- [ ] valider les changements structurants.
