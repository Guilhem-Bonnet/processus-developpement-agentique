# Modèle de pricing registry LLM

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Registry ID | PRICE-... |
| Version | A renseigner |
| Owner | A renseigner |
| Source | provider / pack / projet / manuel |
| Statut | draft / active / superseded / retired |

## Entrées de prix

| Provider | Modèle | Unité | Input price | Output price | Devise | Source | Priorité |
| --- | --- | --- | --- | --- | --- | --- | --- |
| A renseigner | A renseigner | 1M tokens / minute / requête | A renseigner | A renseigner | A renseigner | defaults / pack / projet | 1 / 2 / 3 |

## Application

| Usage | Règle |
| --- | --- |
| Résolution | La couche projet remplace pack, pack remplace defaults. |
| Trace | Chaque appel modèle référence la version de pricing utilisée. |
| Budget | Dépassement déclenche fallback, downgrade, escalade ou blocage. |
| Audit | Les écarts facture/provider sont réconciliés périodiquement. |

## Métriques liées

| Métrique | Usage |
| --- | --- |
| agent_model_tokens_total | Volume token par modèle/provider. |
| agent_model_cost_estimated_total | Coût estimé par mission, rig et modèle. |
| agent_slo_breaches_total | Violations budget ou coût. |

