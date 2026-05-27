# Modèle de registre des providers LLM

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Registry ID | LLMPR-... |
| Projet / organisation | A renseigner |
| Owner | A renseigner |
| Version | A renseigner |
| Statut | draft / active / restricted / deprecated |

## Providers

| Provider ID | Nom | Mode d'accès | Adapter | Statut | Données autorisées | Télémétrie | Fallback |
| --- | --- | --- | --- | --- | --- | --- | --- |
| copilot | GitHub Copilot | ide_integrated / cli | A renseigner | active / restricted | public / interne / selon contrat | limitée / complète / non disponible | A renseigner |
| codex | Codex / OpenAI | api / cli / sdk | A renseigner | active / restricted | A renseigner | tokens / coût / latence / erreurs | A renseigner |
| claude | Anthropic Claude | api / cli / sdk | A renseigner | active / restricted | A renseigner | tokens / coût / latence / erreurs | A renseigner |
| gemini | Google Gemini | api / sdk | A renseigner | active / restricted | A renseigner | tokens / coût / latence / erreurs | A renseigner |
| local | Modèle local | local | A renseigner | active / restricted | local_only | locale | A renseigner |

## Modèles et capacités

| Provider ID | Modèle | Alias autorisés | Capacités | Fenêtre contexte | Outils/function calling | Vision | Statut eval |
| --- | --- | --- | --- | --- | --- | --- | --- |
| A renseigner | A renseigner | A renseigner | code / reasoning / vision / long_context / extraction / critique | A renseigner | oui / non | oui / non | candidate / active / failed |

## Policies

| Policy | Règle |
| --- | --- |
| Provider déclaré | Aucun modèle ne peut être appelé hors registry. |
| Données sensibles | Router uniquement vers provider autorisé ou local_only. |
| Fallback | Fallback entre providers seulement si données, coût, evals et telemetry restent conformes. |
| Alias | Les alias doivent pointer vers un modèle versionné ou un statut explicite. |
| Observabilité | Chaque appel doit tracer provider_id, model_id, adapter, coût, latence, tokens et fallback. |
| Évaluation | Un modèle non évalué ne peut pas être utilisé pour livraison ou décision critique. |

## Cas supportés

| Cas | Configuration minimale |
| --- | --- |
| GitHub Copilot uniquement | Provider `copilot`, modèles exposés par l'environnement, evals par rôle, telemetry disponible documentée. |
| Codex + Claude | Deux providers actifs avec routage par capacité, fallback explicite, policies de données séparées. |
| Multi-fournisseurs | Tous les providers déclarés avec coûts, statuts, adapters, capacités, evals et fallback chain. |

