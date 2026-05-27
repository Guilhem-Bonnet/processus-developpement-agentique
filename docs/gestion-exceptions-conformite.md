# Gestion des exceptions de conformité

Une exception de conformité est un écart temporaire et explicite à une exigence applicable. Elle ne doit pas devenir un contournement permanent du standard.

## Quand créer une exception

| Situation | Exception autorisée ? |
| --- | --- |
| Exigence non applicable au périmètre | non, utiliser not_applicable avec justification. |
| Exigence applicable mais temporairement impossible | oui, avec risque, owner et expiration. |
| Action urgente avec contrôle incomplet | oui, si validation authority accepte le risque. |
| Coût de conformité disproportionné | oui, si risque résiduel documenté. |
| Donnée sensible ou action interdite | non, incident ou blocage. |

## Champs obligatoires

| Champ | Rôle |
| --- | --- |
| exception_id | identifiant stable. |
| requirement_id | exigence concernée. |
| scope | mission, projet, runtime ou organisation. |
| justification | pourquoi l'exception est nécessaire. |
| risk | risque résiduel. |
| compensating_controls | contrôles compensatoires. |
| owner | responsable. |
| approver | autorité qui accepte l'exception. |
| expiry | date, release ou trigger de fin. |
| review_trigger | événement de revue anticipée. |

## Statuts

| Statut | Sens |
| --- | --- |
| requested | exception demandée, non approuvée. |
| approved | exception active et assumée. |
| mitigated | risque réduit par contrôle compensatoire. |
| expired | exception arrivée à échéance. |
| closed | exigence satisfaite ou périmètre retiré. |
| rejected | exception refusée. |

## Règle finale

Une exception sans expiration est une dette de conformité. Une exception sans contrôle compensatoire est un risque accepté à l'aveugle.
