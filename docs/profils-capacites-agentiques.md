# Profils de capacités agentiques

Cette page décrit les capacités minimales attendues d'une structure agentique fonctionnelle. Elle sert de catalogue de capacités, indépendamment d'un outil ou fournisseur précis.

## Catégories de capacités

| Catégorie | But | Exemple de composant |
| --- | --- | --- |
| Mission | Transformer une demande en travail qualifié. | interface de mission, brief, Kanban. |
| Raisonnement | Planifier, comparer, critiquer, décider. | orchestrateur, critique, evals. |
| Contexte | Récupérer et filtrer les informations utiles. | context router, Redis, vector DB, source registry. |
| Action | Lire, écrire, exécuter, appeler des services. | tool registry, MCP gateway, terminal, navigateur. |
| Gouvernance | Autoriser, bloquer, tracer et valider. | policy engine, hooks, RACI. |
| Qualité | Prouver et mesurer. | tests, scans, claim ledger, SLO. |
| Mémoire | Conserver ou oublier correctement. | knowledge janitor, registre de rétention. |

## Profil de capacité : orchestrateur

| Dimension | Exigence |
| --- | --- |
| Entrées | brief, cartes, contexte, règles, métriques. |
| Sorties | plan court, task envelopes, décisions, synthèse. |
| Droits | coordination, lecture contexte, création cartes. |
| Limites | ne valide pas seul les décisions métier ou sensibles. |
| Preuves | journal d'orchestration, handoffs, décisions. |

## Profil de capacité : subagent

| Dimension | Exigence |
| --- | --- |
| Entrées | task envelope, contexte minimal, outils autorisés. |
| Sorties | handoff packet, preuves, risques, limites. |
| Droits | limités au rôle et à la carte. |
| Limites | pas d'action hors périmètre, pas d'escalade implicite. |
| Preuves | sources, commandes, résultats, hypothèses. |

## Profil de capacité : outil

| Dimension | Exigence |
| --- | --- |
| Identification | nom, propriétaire, type, niveau de risque. |
| Autorisation | scopes, conditions d'usage, validation requise. |
| Observabilité | logs, erreurs, coût, durée, sortie utile. |
| Sécurité | secrets masqués, données sensibles minimisées. |
| Reprise | stratégie d'échec, retry, rollback si applicable. |

## Profil de capacité : mémoire

| Dimension | Exigence |
| --- | --- |
| Source | toute entrée durable référence une source. |
| Portée | mission, projet, produit, organisation ou utilisateur. |
| Sensibilité | classification obligatoire. |
| Durée | TTL, valid_until ou revue périodique. |
| Sortie | fait stable ou refus de mémorisation. |

## Profil de capacité : validation

| Dimension | Exigence |
| --- | --- |
| Domaine | métier, architecture, sécurité, UX, ops, QA, mémoire. |
| Autorité | personne, rôle ou règle explicite. |
| Critères | conditions de go/no-go. |
| Preuves | dossier, tests, logs, captures, décisions. |
| Traçabilité | décision, date, limites et risques résiduels. |

## Capacité minimale par type de mission

| Type de mission | Capacités minimales |
| --- | --- |
| Documentation | mission, contexte, claim ledger si affirmation critique, validation documentaire. |
| Code local | mission, contexte workspace, outils locaux, tests, QA. |
| UI / design | mission, sources design, UX/UI/DA, accessibilité, validation visuelle. |
| Sécurité | règles d'engagement, données autorisées, outils contrôlés, rapport de risque. |
| Intégration externe | MCP/tool registry, scopes, logs, dry-run, validation. |
| Production | policy engine strict, dry-run, rollback, observabilité, validation humaine. |
| Mémoire / knowledge base | source registry, rétention, désindexation, knowledge janitor. |
