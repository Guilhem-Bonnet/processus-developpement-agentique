# Checklist d'évaluation de conformité agentique

Cette checklist permet d'évaluer une structure agentique par niveau. Elle peut être utilisée en audit initial, revue périodique ou gate de release.

## Informations d'audit

| Champ | Valeur |
| --- | --- |
| Périmètre | mission / projet / produit / organisation / runtime |
| Niveau visé | 1 / 2 / 3 / 4 / 5 |
| Auditeur | A renseigner |
| Date | A renseigner |
| Sources examinées | A renseigner |

## Niveau 1 : minimal

| Contrôle | Statut | Preuve |
| --- | --- | --- |
| Mission avec objectif, scope et critères | satisfied / partial / failed / n/a | brief, carte. |
| Task envelope pour tâche non triviale | satisfied / partial / failed / n/a | task envelope. |
| Handoff packet structuré | satisfied / partial / failed / n/a | handoff. |
| Preuve de fermeture | satisfied / partial / failed / n/a | evidence item. |
| Validateur identifié | satisfied / partial / failed / n/a | carte, RACI. |

## Niveau 2 : contrôlé

| Contrôle | Statut | Preuve |
| --- | --- | --- |
| Tool registry et permissions | satisfied / partial / failed / n/a | registre outil. |
| Hooks essentiels | satisfied / partial / failed / n/a | hook registry. |
| Secrets et données sensibles protégés | satisfied / partial / failed / n/a | policy, scan, blocage. |
| Claim ledger pour affirmations critiques | satisfied / partial / failed / n/a | claim ledger. |
| Niveau d'autonomie défini | satisfied / partial / failed / n/a | carte, policy. |

## Niveau 3 : orchestré

| Contrôle | Statut | Preuve |
| --- | --- | --- |
| Subagents spécialisés | satisfied / partial / failed / n/a | fiches subagents. |
| Context pack et scorecard | satisfied / partial / failed / n/a | context pack. |
| Model router et fallback | satisfied / partial / failed / n/a | routing policy. |
| Mission ledger | satisfied / partial / failed / n/a | events append-only. |
| Transitions guidées par preuves | satisfied / partial / failed / n/a | verdict, DoD. |

## Niveau 4 : gouverné

| Contrôle | Statut | Preuve |
| --- | --- | --- |
| Evals et SLO | satisfied / partial / failed / n/a | eval report, dashboard. |
| Incidents et reprise | satisfied / partial / failed / n/a | incident record, post-mortem. |
| Rétention et cleanup | satisfied / partial / failed / n/a | retention registry, cleanup report. |
| Validation authorities | satisfied / partial / failed / n/a | RACI, verdicts. |
| Exceptions de conformité | satisfied / partial / failed / n/a | exception records. |

## Niveau 5 : mature

| Contrôle | Statut | Preuve |
| --- | --- | --- |
| Observabilité bout en bout | satisfied / partial / failed / n/a | traces corrélées. |
| Télémétrie exploitable | satisfied / partial / failed / n/a | métriques, logs, événements. |
| Matrices auditables | satisfied / partial / failed / n/a | exigences-preuves, risques-contrôles-preuves. |
| Patterns améliorés par incidents | satisfied / partial / failed / n/a | pattern records, changelog. |
| Audit périodique | satisfied / partial / failed / n/a | audit report. |

## Décision

| Champ | Valeur |
| --- | --- |
| Niveau atteint | 0 / 1 / 2 / 3 / 4 / 5 |
| Écarts bloquants | A renseigner |
| Exceptions acceptées | A renseigner |
| Risques résiduels | A renseigner |
| Prochaine revue | A renseigner |
