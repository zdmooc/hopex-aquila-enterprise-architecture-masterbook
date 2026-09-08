# 13 — Sources officielles et frontière de vérification

## 1. Principe

Cette partie sépare trois niveaux :

### Vérifié publiquement
Information confirmée par une source MEGA accessible publiquement.

### Dépendant de la configuration
Fonction disponible selon solution, rôle, licence ou personnalisation.

### Recommandation pédagogique
Bonne pratique de gouvernance proposée par ce masterbook, sans prétendre qu’elle corresponde à un bouton ou workflow standard identique chez tous les clients.

---

## 2. HOPEX Web Front-End Aquila

Source officielle publique :

- https://store.mega.com/modules/details/hopex.dtpx

Éléments confirmés :

- HOPEX Web Front-End est le portail web HOPEX ;
- il cible notamment enterprise architects, process modelers, risk managers, auditors et stakeholders EA/GRC ;
- la branche actuelle observée est Aquila 6.2 / 62.18.x ;
- build observé : `62.18.0+143`, publié le 2 septembre 2026 ;
- le module dépend de HOPEX Core.

Cette source confirme le rôle du front-end mais ne documente pas publiquement chaque détail de navigation présenté dans une instance client.

---

## 3. HOPEX Core Back-End

Source :

- https://store.mega.com/modules/details/hopex.core

Éléments confirmés :

- Core Back-End Aquila 6.2 ;
- business logic ;
- database access to the repository ;
- connexion des perspectives business, IT, data et risk ;
- positionnement single source of truth ;
- collaboration avec les stakeholders ;
- intégration de la plateforme HOPEX dans l’écosystème numérique.

Cela justifie le principe fondamental de la Partie III :

```text
UI = projection du repository
```

et non :

```text
UI = ensemble indépendant de pages
```

---

## 4. Portfolio de solutions du Web Front-End

Le Store MEGA mentionne notamment :

- HOPEX ITPM ;
- HOPEX ITBM ;
- HOPEX IT Architecture ;
- HOPEX Business Process Analysis ;
- HOPEX Data Governance ;
- HOPEX Information Architecture ;
- HOPEX Integrated Risk Management.

Il mentionne également des capacités d’automatisation, auto-diagramming, dashboards et recommandations dans les versions HOPEX V5/Aquila.

Source :

- https://store.mega.com/modules/details/hopex.dtpx
- https://store.mega.com/bundles/details/b7ff152f-f6dd-4205-bc19-bff1ea2ba0d3

---

## 5. Documentation HOPEX Aquila

La documentation HOPEX est référencée publiquement depuis le Store, notamment vers :

- https://doc.mega.com/hopex-aquila-en

Une partie des contenus dépend d’un accès client/instance. Le masterbook évite donc d’inventer des labels exacts de boutons lorsque la documentation publique ne permet pas de les confirmer.

---

## 6. Ce que cette Partie III affirme avec prudence

Les termes suivants sont utilisés comme concepts d’usage génériques :

- workspace ;
- search ;
- object page ;
- properties ;
- relationships ;
- lists ;
- filters ;
- diagrams ;
- collaboration ;
- validation.

Leur organisation exacte, leur nom, les menus et droits associés peuvent varier selon :

- version ;
- solution HOPEX ;
- persona ;
- licence ;
- métamodèle ;
- configuration client ;
- personnalisation.

Le masterbook enseigne donc **le raisonnement repository derrière l’UI**.

---

## 7. Recommandations pédagogiques non présentées comme fonctions standard

Les éléments suivants sont des pratiques proposées :

- cycle `Draft → Reviewed → Approved → Published` ;
- score de complétude ;
- règles de qualité ;
- date de revue obligatoire ;
- workflow MayaBank de validation ;
- workspace type par persona ;
- seuils de stale data ;
- listes de contrôle qualité ;
- nomenclature de packs Architecture Board.

Ils doivent être implémentés avec les mécanismes réellement disponibles chez le client.

---

## 8. Règle pour les prochaines parties

À chaque fois qu’un chapitre décrit un comportement HOPEX :

```text
1. vérifier le produit / module public
2. identifier ce qui dépend d’une licence/configuration
3. ne pas inventer un écran exact
4. séparer pratique EA et fonction produit
5. utiliser MayaBank comme cas pédagogique, jamais comme preuve produit
```

Cette règle sera particulièrement importante pour :

- Partie IV — IT Architecture ;
- Partie XIII — ITBM/APM ;
- Partie XIV — ITPM ;
- Partie XVII — administration et droits ;
- Partie XVIII — customization ;
- Partie XX — REST/GraphQL/ServiceNow/MCP.
