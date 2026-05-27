# Modèle de workflow state manifest

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Workflow ID | WF-... |
| Nom | A renseigner |
| Owner | A renseigner |
| Version | A renseigner |
| Profil | minimal / orchestré / gouverné / production |
| Statut | draft / active / deprecated / retired |

## États

| État | Rôle | Entrées requises | Sorties attendues | Preuve minimale |
| --- | --- | --- | --- | --- |
| intake | Qualifier la mission. | brief | DoR | brief validé |
| discovery | Explorer sources et risques. | DoR, sources | options / questions | context scorecard |
| implementation | Produire le changement. | décision, task envelope | artefact | diff / trace / test |
| verification | Vérifier le résultat. | evidence pack | verdict | verification verdict |

## Transitions

| De | Vers | Guard | Retry | Compensation | Autorité |
| --- | --- | --- | --- | --- | --- |
| A renseigner | A renseigner | preuve / policy / score | none / bounded | rollback / correction | orchestrateur / humain |

## Interruptions

| Interrupt | Quand | Choix permis | Reprise |
| --- | --- | --- | --- |
| human_required | décision métier ou risque élevé | accepter / refuser / préciser | état précédent ou état ciblé |
| evidence_missing | preuve absente | compléter / rouvrir / escalader | verification |

## Télémétrie

| Signal | Attributs |
| --- | --- |
| workflow.state.entered | workflow_id, state, actor, mission_id |
| workflow.transition.requested | from, to, guard, evidence_pack_id |
| workflow.transition.blocked | reason, missing_evidence, policy |
| workflow.interrupted | interrupt_type, authority, resume_state |

