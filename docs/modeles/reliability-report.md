# Modèle de reliability report agentique

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Report ID | REL-... |
| Période | A renseigner |
| Scope | mission / projet / organisation |
| Runtime provider | local / tmux / subprocess / Kubernetes / autre |

## Agrégation

| Model | Prompt version | Rig | Sessions | Crashed | Quarantined | Idle killed | Drained | CrashRate% | UnhealthyRate% |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A renseigner | A renseigner | A renseigner | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

## Décisions

| Condition | Décision |
| --- | --- |
| CrashRate% dépasse seuil | Quarantine, rollback prompt, fallback modèle ou incident. |
| UnhealthyRate% dépasse seuil | Réduire capacité, inspecter rig, ouvrir remediation. |
| Idle killed élevé | Ajuster timeout, budget ou découpage des tâches. |

## Preuves liées

| Preuve | Source |
| --- | --- |
| Event `runtime.session_unhealthy` | telemetry event |
| Rapport de quarantine | runtime provider |
| Incident ou remediation | incident-agentique / mission ledger |

