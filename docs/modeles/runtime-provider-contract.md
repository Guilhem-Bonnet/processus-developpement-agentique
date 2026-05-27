# Modèle de runtime provider contract

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Provider ID | RTP-... |
| Type | local / subprocess / tmux / ACP / Kubernetes / remote |
| Owner | A renseigner |
| Statut | draft / active / restricted / retired |

## Lifecycle

| Phase | Contrat |
| --- | --- |
| prepare | Vérifier workspace, secrets autorisés, ressources et policy. |
| spawn | Démarrer session avec env scrub, quotas et trace_id. |
| execute | Exposer commandes/outils autorisés seulement. |
| observe | Publier logs, events, health, coût et durée. |
| stop | Arrêt normal, timeout, cancellation ou quarantine. |
| cleanup | Purge artefacts temporaires, secrets et ressources. |

## Ressources

| Ressource | Limite | Preuve |
| --- | --- | --- |
| CPU / mémoire | A renseigner | métriques runtime |
| Fichiers | paths allow/deny | policy decision |
| Réseau | allowlist / denylist | logs egress |
| Secrets | scoped / denied | env scrub event |

## Health

| Signal | Seuil |
| --- | --- |
| crash_rate | A renseigner |
| unhealthy_rate | A renseigner |
| idle_timeout | A renseigner |
| max_duration | A renseigner |

