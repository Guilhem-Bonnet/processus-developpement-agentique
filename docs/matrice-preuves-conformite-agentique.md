# Matrice de preuves de conformité agentique

Cette page rend les niveaux de conformité vérifiables. Une structure agentique ne doit pas seulement déclarer qu'elle est gouvernée : elle doit montrer les preuves qui satisfont chaque famille d'exigences.

## Principe

Toute exigence normative DOIT pouvoir pointer vers au moins une preuve attendue : document, manifeste, hook, policy, test, eval, evidence pack, journal ou décision de validation.

## Matrice par domaine

| Domaine | Exigences | Preuves attendues |
| --- | --- | --- |
| Mission | AG-MIS | brief, mission ledger, carte Kanban, critères d'acceptation. |
| Orchestration | AG-ORC | task envelope, handoff packet, workflow, trace de délégation. |
| Contexte | AG-CTX | context profile, context pack, source registry, logs de récupération, metadata de fraîcheur. |
| Modèles | AG-LLM | politique de routage, fallback, evals modèle, journal d'appel. |
| Outils | AG-TOL | tool registry, policy request, MCP contract, hook pre-tool. |
| Qualité | AG-QUA | claim ledger, evidence pack, verification verdict, dossier d'acceptation. |
| Incidents | AG-INC | rapport incident, rollback, purge mémoire, post-mortem, eval de prévention. |
| Rétention | AG-RET | registre de rétention, TTL, archive, désindexation, cleanup report. |
| Patterns | AG-PAT | catalogue de patterns, lifecycle, matrice patterns-exigences-preuves, preuves d'usage. |
| Audit | AG-AUD | audit report, checklist de conformité, exceptions, matrice risques-contrôles-preuves. |
| Observabilité | AG-OBS | traces corrélées, métriques, logs, telemetry events, dashboards, alertes SLO. |

## Statuts de conformité

| Statut | Sens |
| --- | --- |
| satisfied | exigence couverte par preuve active. |
| partial | exigence couverte partiellement ou seulement manuellement. |
| planned | exigence identifiée avec plan mais sans preuve. |
| not_applicable | exigence hors périmètre déclaré. |
| non_conformant | exigence applicable non satisfaite. |

## Fiche de conformité par exigence

| Champ | Description |
| --- | --- |
| requirement_id | identifiant AG-*. |
| status | satisfied, partial, planned, not_applicable, non_conformant. |
| evidence_refs | fichiers, journaux, manifests, packs ou décisions. |
| owner | rôle responsable. |
| scope | mission, projet, runtime, produit, organisation. |
| residual_risk | risque restant. |
| next_action | action de mise en conformité. |
| review_trigger | événement déclenchant une revue. |

## Exemples de preuves acceptables

| Preuve | Couvre |
| --- | --- |
| Agent manifest | rôles, capacités, subagents. |
| Workflow manifest | orchestration, étapes, transitions. |
| Tool manifest | outils, risques, permissions. |
| MCP policy | intégrations externes, scopes, fail-closed. |
| Hook registry | contrôles pre/post action, modes shadow/canary/enforced. |
| Model routing policy | routage modèle, fallback, retrait modèle. |
| Mission ledger | mission, tâche, transition, incident. |
| Evidence pack | preuves typées et couverture. |
| Verification verdict | décision de fermeture ou réouverture. |
| Context pack | sources incluses/exclues, scorecard, contraintes et confiance. |
| Pattern matrix | lien entre patterns, exigences et preuves. |
| Control record | définition d'un contrôle, déclencheur, preuve et télémétrie. |
| Telemetry event | événement corrélé à mission, tâche, contrôle, preuve ou incident. |
| Audit report | niveau atteint, écarts, exceptions et risques résiduels. |
| Exception record | justification, risque, contrôles compensatoires et expiration. |
| Memory audit | obsolescence, secrets, désindexation. |
| Retention registry | destination durable, archive, TTL ou purge. |
| Acceptance dossier | acceptation client et risques résiduels. |

## Niveaux de conformité vérifiables

| Niveau | Preuves minimales |
| --- | --- |
| 1 Minimal | brief, carte, task envelope, handoff, preuve de fermeture. |
| 2 Contrôlé | tool registry, hooks essentiels, permissions, risques IA. |
| 3 Orchestré | subagents, context router, model router, workflow manifest. |
| 4 Gouverné | evals, SLO, incidents, rétention, validation authority. |
| 5 Mature | observabilité bout en bout, télémétrie corrélée, memory gate, doc drift, audit périodique. |

## Contrôle de dérive documentaire

La conformité doit être revue si :

- un agent, outil, hook ou workflow est ajouté ;
- une politique de sécurité change ;
- un modèle LLM est retiré ou remplacé ;
- une source de vérité est superseded ;
- un incident révèle un faux Done ou une mémoire polluée ;
- un document normatif change.

## Règle finale

Une exigence sans preuve est une intention. Une preuve sans exigence est un artefact isolé. La conformité agentique commence quand chaque exigence importante possède une preuve active, maintenue et révisable.
