# Modèle de traçabilité agentique

La traçabilité relie le besoin initial à la preuve finale. Elle permet d'expliquer pourquoi une action a été prise, quels contrôles l'ont encadrée et comment le résultat a été accepté.

## Chaîne minimale

| Maillon | Artefact |
| --- | --- |
| Besoin | demande client, brief. |
| Exigence | AG-* ou critère d'acceptation. |
| Pattern | pattern appliqué. |
| Contrôle | hook, gate, validation, eval, policy. |
| Exécution | task envelope, outil, modèle, subagent. |
| Contexte | context pack, sources, scorecard. |
| Preuve | claim ledger, evidence pack, trace. |
| Verdict | verification verdict. |
| Acceptation | dossier d'acceptation ou décision client. |
| Amélioration | incident, eval, pattern update ou backlog. |

## Identifiants recommandés

| Préfixe | Artefact |
| --- | --- |
| MIS | mission. |
| REQ | exigence projet ou critère. |
| AG | exigence normative. |
| PAT | pattern record. |
| CTRL | contrôle. |
| CTX | context pack. |
| TASK | task envelope ou carte. |
| HND | handoff packet. |
| EVD | evidence pack. |
| VER | verification verdict. |
| INC | incident. |
| EXC | exception. |
| TEL | événement télémétrique. |

## Traceability record

| Champ | Description |
| --- | --- |
| trace_id | identifiant de corrélation. |
| mission_id | mission liée. |
| requirement_refs | exigences et critères. |
| pattern_refs | patterns appliqués. |
| control_refs | contrôles déclenchés. |
| context_pack_refs | contexte utilisé. |
| evidence_refs | preuves produites. |
| verdict_ref | décision de vérification. |
| telemetry_refs | traces, métriques ou logs liés. |
| residual_risk | risque restant. |

## Règle finale

Une décision agentique durable doit être traçable de son besoin à sa preuve. Si un maillon manque, la confiance doit baisser ou une exception doit être ouverte.
