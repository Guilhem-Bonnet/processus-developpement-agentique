# Modèle de contrat controller-agent privilege

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Contract ID | CAPC-... |
| Controller | A renseigner |
| Runtime provider | local / tmux / subprocess / exec / ACP / Kubernetes |
| Scope | mission / projet / organisation |
| Statut | draft / active / enforced / retired |

## Permissions

| Élément | Controller | Agent | Règle |
| --- | --- | --- | --- |
| Clés `convergence.*` | read/write | read-only / denied | A renseigner |
| Clés `var.*` | read/write | read-only / denied | A renseigner |
| Tokens provider | allowed | denied | scrub avant spawn |
| Secrets projet | selon politique | minimisés | injecter seulement si requis |
| État runtime | reconcile | report | agent ne modifie pas l'état d'infrastructure |

## Scrub d'environnement

| Variable ou pattern | Action | Justification |
| --- | --- | --- |
| CONTROLLER_TOKEN | remove | Empêcher écriture infrastructure par l'agent. |
| *_ADMIN_TOKEN | remove / mask | A renseigner. |
| *_SERVICE_ACCOUNT | remove / scoped | A renseigner. |

## Preuves attendues

| Preuve | Source |
| --- | --- |
| Event `runtime.controller_token_scrubbed` | telemetry event |
| Log de spawn sans secret controller | runtime provider |
| Refus d'écriture agent sur clé protégée | policy engine |

