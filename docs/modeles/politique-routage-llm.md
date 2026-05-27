# Modèle de politique de routage LLM

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Projet ou mission | A renseigner |
| Propriétaire | A renseigner |
| Date | A renseigner |
| Version | A renseigner |
| Portée | workspace / produit / équipe / agent |

## Modèles autorisés

### Providers autorisés

| Provider | Mode d'accès | Modèles exposés | Données autorisées | Télémétrie | Statut | Fallback provider |
| --- | --- | --- | --- | --- | --- | --- |
| A renseigner | api / ide_integrated / cli / mcp / local / internal_gateway | A renseigner | public / interne / confidentiel / local seulement | prompts / tokens / coût / latence / limité | active / restricted / deprecated / disallowed | A renseigner |

| Modèle | Usage autorisé | Données autorisées | Coût cible | Limites | Fallback |
| --- | --- | --- | --- | --- | --- |
| A renseigner | triage / code / architecture / critique / vision / sécurité | public / interne / confidentiel / local seulement | A renseigner | A renseigner | A renseigner |

## Matrice tâche -> modèle

| Tâche | Provider principal | Modèle principal | Capacité requise | Budget contexte | Validation | Fallback |
| --- | --- | --- | --- | --- | --- | --- |
| Triage Kanban | A renseigner | A renseigner | classification | tiny | échantillonnage | A renseigner |
| Discovery / cadrage | A renseigner | A renseigner | raisonnement / synthèse | medium | analyste/client | A renseigner |
| Architecture | A renseigner | A renseigner | raisonnement profond | deep | critique/architecte | A renseigner |
| Implémentation | A renseigner | A renseigner | code | small/medium | tests/QA | A renseigner |
| QA / critique | A renseigner | A renseigner | critique / contradiction | medium | scorecard | A renseigner |
| Sécurité | A renseigner | A renseigner | sécurité / localité | medium | sécurité | A renseigner |
| UI / vision | A renseigner | A renseigner | vision | medium | design/DA | A renseigner |
| Documentation | A renseigner | A renseigner | rédaction / synthèse | small | diagnostics/liens | A renseigner |
| Capitalisation mémoire | A renseigner | A renseigner | extraction conservatrice | tiny/small | pre-memory-write | ne pas mémoriser |

## Règles de décision

| Condition | Décision |
| --- | --- |
| Donnée sensible | modèle local ou autorisé contractuellement. |
| Provider non déclaré | bloquer : aucun modèle ne doit être appelé hors provider registry. |
| Coût supérieur au budget | compression, réduction contexte ou validation. |
| Risque élevé | modèle profond + critique + validation humaine. |
| Réponse instable | relance stricte, modèle alternatif ou revue. |
| Modèle non évalué | interdit pour livraison. |
| Divergence entre modèles | escalade au critique ou validateur. |

## Evals requises

| Modèle | Eval | Seuil | Statut |
| --- | --- | --- | --- |
| A renseigner | A renseigner | A renseigner | à faire / passé / échoué |

## Journal de changement

| Version | Changement | Raison | Validation |
| --- | --- | --- | --- |
| 0.1 | création | A renseigner | A renseigner |
