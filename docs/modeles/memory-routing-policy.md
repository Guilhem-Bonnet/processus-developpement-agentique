# Modèle de memory routing policy

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Policy ID | MRP-... |
| Scope | mission / projet / organisation |
| Owner | A renseigner |
| Version | A renseigner |

## Couches

| Couche | Usage | Peut fermer une décision ? |
| --- | --- | --- |
| L0 fenêtre active | objectif immédiat | non |
| L1 contexte chaud | état mission, cache, Kanban | non seul |
| L2 base de connaissance indexée | corpus externe gouverné | seulement avec source active |
| L3 mémoire agentique durable | apprentissages sourcés | non seul |
| Graphe / sidecar | relations, validité, confiance | non seul |
| Source de vérité | docs/code/tests/ADR actifs | oui |

## Routage

| Situation | Couche prioritaire | Contrôle |
| --- | --- | --- |
| Décision critique | source de vérité | preuve obligatoire |
| Recherche domaine | base de connaissance indexée | ACL + freshness |
| Reprise mission | contexte chaud + mission ledger | TTL + mission_id |
| Capitalisation | mémoire durable | promotion gate |
| Contradiction | graphe + source active | conflict resolver |

