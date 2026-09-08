# 05 — MetaAssociation, Ends & Cardinality

## 1. Une relation porte une sémantique

Le repository HOPEX n'est pas seulement une liste d'objets. Sa valeur vient du graphe de relations.

```text
Application → supports → Business Capability
Application → uses → Software Technology
Org-Unit → owns → Application
Business Process → uses → Application
```

Les libellés exacts doivent être pris dans le métamodèle installé.

## 2. Concepts vérifiés

L'endpoint public MetaModel renvoie notamment :

```text
MetaAssociation
MetaAssociationEnd
MetaAssociationType
```

Cela confirme que les associations et leurs extrémités font partie du métamodèle explicite de HOPEX.

## 3. Pourquoi deux extrémités ?

Une relation doit être compréhensible dans les deux sens.

Exemple pédagogique :

```text
Application -- supports --> Capability
Capability  -- supported by --> Application
```

Le sens de lecture inverse est indispensable pour :

- navigation ;
- impact analysis ;
- matrices ;
- queries GraphQL ;
- rapports.

## 4. Cardinalité

Une association peut conceptuellement contraindre le nombre d'objets liés.

Exemples possibles selon métamodèle :

```text
1 owner pour une application
0..n technologies pour une application
0..n applications pour une capability
```

Ne jamais inventer la cardinalité réelle sans consulter le métamodèle ou la documentation cible.

## 5. Relation directe vs objet intermédiaire

Parfois une relation simple suffit :

```text
Application → Business Capability
```

Parfois il faut modéliser un concept intermédiaire car il porte ses propres données :

```text
Application
→ Interface / Flow
→ Application
```

ou :

```text
Application
→ Deployment
→ Technology environment
```

Règle : créer un objet intermédiaire seulement s'il a une sémantique ou des propriétés utiles.

## 6. Relation n'est pas propriété

Mauvais :

```text
Application.OwnerName = "Payments IT"
```

si `Payments IT` est lui-même une Org-Unit gouvernée.

Meilleur :

```text
Application
→ owned by
→ Org-Unit Payments IT
```

Pourquoi ?

Parce que l'Org-Unit devient réutilisable et analysable.

## 7. Relation n'est pas texte

Mauvais :

```text
Description = "Uses Kafka and PostgreSQL"
```

si l'objectif est d'analyser les dépendances technologiques.

Meilleur :

```text
Application
→ uses Software Technology Kafka
→ uses Software Technology PostgreSQL
```

## 8. Relations minimales

Plus de relations n'est pas toujours mieux.

Un graphe saturé :

```text
chaque objet ↔ chaque objet
```

rend les analyses inutilisables.

Créer uniquement les relations qui :

- ont une définition ;
- servent une question ;
- ont une source ;
- peuvent être maintenues.

## 9. MayaBank — graphe cible simplifié

```text
Real-Time Payment Capability
        ↑
Execute Instant Payment Process
        ↑
Payment Orchestrator
   ├─ uses Fraud Engine
   ├─ uses Event Streaming Platform
   ├─ uses Payment Database
   └─ owned by Payments Domain
```

Ce graphe sera ensuite raffiné avec les classes et relations HOPEX réellement utilisées dans les parties spécialisées.

## 10. Impact analysis

Si `Event Streaming Platform` est retirée :

```text
Technology retire
→ applications dépendantes
→ processes supportés
→ capabilities impactées
→ projects de remplacement
```

C'est exactement le type de navigation qu'un repository structuré rend possible.

## 11. Matrices

Une relation structurée peut alimenter :

```text
Applications × Capabilities
Applications × Technologies
Applications × Org-Units
Applications × Data
Processes × Applications
```

Une relation stockée dans une description ne le peut pas correctement.

## 12. Anti-patterns

- Association générique utilisée pour tout ;
- relation dupliquée dans deux sens avec deux objets différents ;
- relation sans définition ;
- relation importée sans source ;
- relation runtime éphémère synchronisée dans l'EAM sans besoin ;
- relations manuelles qui contredisent une source automatique ;
- objet intermédiaire créé uniquement pour dessiner une ligne.

## 13. Questions d'entretien

**Pourquoi les relations sont-elles plus importantes que les diagrammes ?**  
Parce qu'elles structurent le graphe réutilisable par les analyses, APIs, matrices et vues.

**Pourquoi MetaAssociationEnd ?**  
Parce qu'une association doit pouvoir être interprétée depuis chaque extrémité et naviguée dans les deux sens selon le métamodèle.
