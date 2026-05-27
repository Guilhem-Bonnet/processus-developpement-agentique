# Modèle de source graph record

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Graph ID | SG-... |
| Source | A renseigner |
| Owner | A renseigner |
| Version | A renseigner |
| Statut | candidate / active / stale / quarantined |

## Nœuds

| Node ID | Type | Référence | Statut | Sensibilité |
| --- | --- | --- | --- | --- |
| A renseigner | doc / code / ADR / ticket / API / preuve | A renseigner | active / superseded / obsolete | A renseigner |

## Relations

| Source | Relation | Cible | Confiance | Preuve |
| --- | --- | --- | --- | --- |
| A renseigner | depends_on / contradicts / supersedes / proves / implements | A renseigner | high / medium / low | A renseigner |

## Contrôles

| Contrôle | Règle |
| --- | --- |
| Provenance | Chaque relation doit pointer vers source ou preuve. |
| Fraîcheur | Les nœuds stale ne peuvent pas fermer une décision. |
| Contradiction | Les contradictions critiques bloquent le verdict durable. |

