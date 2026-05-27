# Catalogue des contrôles agentiques

Le catalogue des contrôles décrit les mécanismes qui réduisent les risques agentiques. Un contrôle doit avoir un objectif, un moment d'application, une preuve et une réaction en cas d'échec.

## Familles de contrôles

| Famille | Usage |
| --- | --- |
| Prévention | Empêcher une action non autorisée avant exécution. |
| Détection | Identifier dérive, erreur, contradiction ou incident. |
| Validation | Obtenir une décision humaine ou agentique autorisée. |
| Preuve | Produire un artefact vérifiable. |
| Rétention | Décider ce qui est gardé, archivé, désindexé ou purgé. |
| Télémétrie | Mesurer traces, métriques, logs et événements. |
| Amélioration | Transformer incident ou métrique en eval, hook, pattern ou correction. |

## Contrôles principaux

| ID | Contrôle | Type | Déclenchement | Preuve |
| --- | --- | --- | --- | --- |
| CTRL-MIS-001 | Mission readiness gate | prévention | avant création de lot | brief complet, critères, scope. |
| CTRL-CTX-001 | Pre-context-load | prévention | avant récupération contexte | context profile, sources autorisées. |
| CTRL-CTX-002 | Context scorecard | détection | après récupération contexte | score suffisance, fraîcheur, cohérence. |
| CTRL-CTX-003 | Conflict resolution gate | validation | contradiction critique | décision, hypothèse ou escalade. |
| CTRL-CTX-004 | Budget escalation gate | prévention | passage small/medium/deep | justification coût/risque. |
| CTRL-MOD-001 | Pre-model-route | prévention | avant appel modèle | modèle autorisé, fallback. |
| CTRL-MOD-002 | Model retirement guard | prévention | modèle deprecated/disallowed | fallback ou rejet. |
| CTRL-TOL-001 | Pre-tool policy | prévention | avant appel outil | décision allow/block/escalate. |
| CTRL-TOL-002 | Tool blast-radius limiter | prévention | outil risqué | périmètre fichiers, env, réseau, coût. |
| CTRL-SEC-001 | Secret and PII guard | prévention | prompt, outil, mémoire, log | masquage, blocage, incident. |
| CTRL-SEC-002 | Prompt injection firewall | prévention | contenu externe non fiable | contenu isolé, instructions non modifiées. |
| CTRL-SEC-003 | No token proxy guard | prévention | coordination locale ou spawn agent | env scrub, token non transmis. |
| CTRL-AUT-001 | Autonomy level gate | prévention | carte non triviale | niveau A0-A5 et justification. |
| CTRL-DRY-001 | Dry-run gate | validation | action destructive/externe/coûteuse | impact, rollback, go/no-go. |
| CTRL-DRY-002 | Cluster dry-run gate | validation | action cluster ou cloud | diff, RBAC, impact, rollback. |
| CTRL-QUA-001 | Claim ledger check | preuve | affirmation critique | source, preuve ou hypothèse. |
| CTRL-QUA-002 | Evidence pack gate | preuve | fermeture ou livraison | preuves liées aux critères. |
| CTRL-QUA-003 | Verification verdict gate | validation | tâche à risque | close/reopen/incident/escalate. |
| CTRL-OBS-001 | Trace completeness check | détection | fin de run | spans mission, contexte, outil, verdict. |
| CTRL-OBS-002 | Telemetry privacy gate | prévention | export traces/logs | secrets masqués, minimisation. |
| CTRL-OBS-003 | Trajectory completeness check | détection | fin de mission à risque | intention, action, observation, verdict. |
| CTRL-SLO-001 | SLO breach alert | détection | seuil qualité/coût/latence | alerte, carte correction. |
| CTRL-RET-001 | Pre-memory-write | prévention | écriture mémoire | source, stabilité, sensibilité, TTL. |
| CTRL-RET-002 | Scheduled cleanup | amélioration | périodique | rapport cleanup, désindexation. |
| CTRL-SRC-001 | Remote hygiene guard | prévention | audit/indexation source distante | remote, ref, dirty state, fraîcheur. |
| CTRL-UI-001 | Visual evidence gate | preuve | validation UI/browser | screenshot, DOM, logs. |
| CTRL-EVL-001 | Eval lifecycle gate | validation | promotion prompt/modèle/skill | dataset, seuil, historique. |
| CTRL-INC-001 | Incident containment | prévention | anomalie critique | autonomie réduite, blocage, owner. |
| CTRL-PAT-001 | Pattern lifecycle review | amélioration | release, incident, audit | pattern record mis à jour. |

## Fiche minimale d'un contrôle

| Champ | Description |
| --- | --- |
| control_id | identifiant stable. |
| objective | risque réduit ou décision sécurisée. |
| trigger | moment d'application. |
| owner | rôle responsable. |
| input | artefacts nécessaires. |
| decision | allow, block, escalate, observe, pass, fail. |
| evidence | preuve produite. |
| telemetry | trace, métrique, log ou événement attendu. |
| failure_response | action si le contrôle échoue. |

## Règle finale

Un contrôle non observable est difficile à auditer. Un contrôle sans réaction d'échec est seulement un conseil.
