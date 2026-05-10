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

| Modèle | Usage autorisé | Données autorisées | Coût cible | Limites | Fallback |
| --- | --- | --- | --- | --- | --- |
| A renseigner | triage / code / architecture / critique / vision / sécurité | public / interne / confidentiel / local seulement | A renseigner | A renseigner | A renseigner |

## Matrice tâche -> modèle

| Tâche | Modèle principal | Budget contexte | Validation | Fallback |
| --- | --- | --- | --- | --- |
| Triage Kanban | A renseigner | tiny | échantillonnage | A renseigner |
| Discovery / cadrage | A renseigner | medium | analyste/client | A renseigner |
| Architecture | A renseigner | deep | critique/architecte | A renseigner |
| Implémentation | A renseigner | small/medium | tests/QA | A renseigner |
| QA / critique | A renseigner | medium | scorecard | A renseigner |
| Sécurité | A renseigner | medium | sécurité | A renseigner |
| UI / vision | A renseigner | medium | design/DA | A renseigner |
| Documentation | A renseigner | small | diagnostics/liens | A renseigner |
| Capitalisation mémoire | A renseigner | tiny/small | pre-memory-write | ne pas mémoriser |

## Règles de décision

| Condition | Décision |
| --- | --- |
| Donnée sensible | modèle local ou autorisé contractuellement. |
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
