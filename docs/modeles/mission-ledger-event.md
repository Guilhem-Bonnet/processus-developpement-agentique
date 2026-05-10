# Modèle d'événement de mission ledger

## Événement

| Champ | Valeur |
| --- | --- |
| Event ID | evt-... |
| Type | mission.created / task.created / task.transitioned / evidence.attached / incident.created |
| Entity ID | A renseigner |
| Entity kind | mission / task / evidence / incident / decision |
| Actor ID | A renseigner |
| Date | A renseigner |
| Schema version | agentic.ledger_event.v1 |

## Payload

| Champ | Valeur |
| --- | --- |
| Mission ID | A renseigner |
| Task ID | A renseigner |
| Ancien état | A renseigner |
| Nouvel état | A renseigner |
| Raison | A renseigner |
| Preuve liée | A renseigner |
| Risque | A renseigner |

## Règles

- Un événement est append-only.
- Une transition doit respecter la machine d'état déclarée.
- Une fermeture doit pointer vers un evidence pack ou un verdict.
- Un incident doit pointer vers la tâche ou mission impactée.
