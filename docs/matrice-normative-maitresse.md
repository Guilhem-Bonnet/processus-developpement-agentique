# Matrice normative maîtresse

Cette matrice est la table de pilotage normative. Elle relie chaque famille d'exigences à un profil de conformité, aux preuves attendues, aux patterns et aux contrôles principaux.

## Lecture

| Colonne | Sens |
| --- | --- |
| ID | Exigence ou plage d'exigences normative. |
| Obligation | Résumé normatif. |
| Profil | Premier niveau où l'exigence devient attendue. |
| Preuves minimales | Artefacts acceptables pour démontrer la conformité. |
| Patterns | Patterns principaux qui réalisent ou structurent l'exigence. |
| Contrôles | Contrôles principaux qui vérifient ou bloquent. |

## Matrice

| ID | Obligation | Profil | Preuves minimales | Patterns | Contrôles |
| --- | --- | --- | --- | --- | --- |
| AG-MIS-001 | Toute mission DOIT avoir un objectif explicite. | N1 | brief agentique | ORG-01 | CTRL-MIS-001 |
| AG-MIS-002 | Toute mission DOIT définir périmètre et hors-scope. | N1 | brief, carte Kanban | ORG-01 | CTRL-MIS-001 |
| AG-MIS-003 | Toute mission DOIT posséder des critères vérifiables. | N1 | critères d'acceptation, evidence pack attendu | ORG-01, QUA-04 | CTRL-MIS-001, CTRL-QUA-002 |
| AG-MIS-004 | Toute mission DEVRAIT identifier valeur, utilisateurs et contraintes. | N1 | brief enrichi | ORG-01 | CTRL-MIS-001 |
| AG-MIS-005 | Toute ambiguïté bloquante DOIT être résolue par contexte vérifié ou question ciblée. | N2 | question ciblée, context pack, hypothèse | ORC-07 | CTRL-CTX-003 |
| AG-ORC-001 | Toute tâche non triviale DOIT être représentée par carte ou lot traçable. | N1 | carte Kanban, mission ledger | ORC-01, ORC-09 | CTRL-MIS-001 |
| AG-ORC-002 | Toute délégation à un subagent DOIT utiliser un task envelope. | N1 | task envelope | ORC-02 | CTRL-TOL-001 |
| AG-ORC-003 | Tout subagent DOIT produire un handoff packet structuré. | N1 | handoff packet | ORC-03 | CTRL-QUA-001 |
| AG-ORC-004 | L'orchestrateur DOIT limiter le WIP et éviter les délégations ouvertes. | N3 | WIP, queue, worker pool status | ORC-01, RUN-10 | CTRL-OBS-001 |
| AG-ORC-005 | Les communications inter-agents DOIVENT être tracées si elles influencent une décision. | N3 | mission ledger, trajectory log | ORC-01, QUA-10 | CTRL-OBS-003 |
| AG-ORC-006 | Les transitions DEVRAIENT être journalisées dans un ledger append-only. | N3 | mission ledger event | QUA-03, ORC-09 | CTRL-QUA-003 |
| AG-CTX-001 | Le contexte fourni DOIT être proportionné au rôle. | N2 | context profile, context pack | ORC-04, ORC-08 | CTRL-CTX-001 |
| AG-CTX-002 | Une source critique DOIT avoir provenance, date, statut et propriétaire. | N2 | source registry, knowledge source index | ORC-06, KNO-06 | CTRL-CTX-001, CTRL-SRC-001 |
| AG-CTX-003 | Une base vectorielle DOIT être traitée comme rappel, pas vérité. | N2 | context constitution, source active | ORC-06, KNO-02 | CTRL-CTX-003 |
| AG-CTX-004 | Le contexte chaud DOIT avoir TTL et portée de mission. | N2 | cache metadata, mission_id, TTL | KNO-02 | CTRL-RET-002 |
| AG-CTX-005 | Toute source obsolète, remplacée ou sensible DOIT être bloquée ou désindexée. | N2 | freshness report, désindexation | KNO-01, GOV-13 | CTRL-RET-002 |
| AG-CTX-006 | Une mémoire durable DOIT être stable, sourcée et minimisée. | N2 | memory record, promotion decision | KNO-04 | CTRL-RET-001 |
| AG-CTX-007 | Une mémoire mature DEVRAIT distinguer vectoriel, graphe, faits temporels et vérité. | N4 | memory routing policy, source graph | KNO-02, KNO-08 | CTRL-CTX-003 |
| AG-CTX-008 | Toute lecture mémoire critique DOIT vérifier statut, validité et source active. | N2 | memory audit, source check | KNO-07, KNO-10 | CTRL-CTX-003 |
| AG-CTX-009 | Une structure avancée DEVRAIT disposer d'un orchestrateur de contexte. | N4 | context scorecard, decision log | ORC-05 | CTRL-CTX-001 |
| AG-CTX-010 | Tout context pack à risque DOIT identifier sources incluses/exclues, contraintes et confiance. | N3 | context pack | ORC-05, ORC-06 | CTRL-CTX-002 |
| AG-CTX-011 | Toute contradiction critique DOIT être résolue, portée comme hypothèse ou escaladée. | N2 | contradiction report | ORC-07, KNO-10 | CTRL-CTX-003 |
| AG-CTX-012 | Toute augmentation de budget contexte DEVRAIT être justifiée. | N2 | budget escalation record | ORC-08 | CTRL-CTX-004 |
| AG-LLM-001 | Le choix du modèle DOIT dépendre tâche, risque, coût et confidentialité. | N3 | routing policy, provider registry | MOD-01 | CTRL-MOD-001 |
| AG-LLM-002 | Toute tâche à risque DOIT définir fallback ou escalade. | N3 | fallback chain, escalation rule | MOD-01, GOV-14 | CTRL-MOD-001 |
| AG-LLM-003 | Un modèle pour décision durable DEVRAIT avoir des evals représentatives. | N4 | eval dataset record | QUA-13 | CTRL-EVL-001 |
| AG-LLM-004 | Les appels modèle DOIVENT être journalisés. | N3 | telemetry event, cost span | QUA-08, QUA-06 | CTRL-OBS-001 |
| AG-LLM-005 | Les données sensibles NE DOIVENT PAS être transmises à un modèle non autorisé. | N2 | provider data policy, blocked call | MOD-01, GOV-12 | CTRL-SEC-001 |
| AG-LLM-006 | Les modèles dépréciés/interdits DOIVENT déclencher fallback ou rejet. | N4 | model status, fallback event | MOD-02 | CTRL-MOD-002 |
| AG-TOL-001 | Tout outil DOIT être inscrit avec risque et permissions. | N2 | tool registry, MCP contract | GOV-07, GOV-09 | CTRL-TOL-001 |
| AG-TOL-002 | Toute action destructive/externe/coûteuse DOIT passer par hook ou validation. | N2 | policy decision, dry-run | GOV-02, GOV-07 | CTRL-TOL-002, CTRL-DRY-001 |
| AG-TOL-003 | Les intégrations MCP DOIVENT définir owner, scopes, timeout et logs. | N2 | contrat MCP | GOV-09 | CTRL-TOL-001 |
| AG-TOL-004 | Les secrets NE DOIVENT PAS être exposés. | N2 | redaction, secret block, env scrub | GOV-05, RUN-12 | CTRL-SEC-001, CTRL-SEC-003 |
| AG-TOL-005 | Les erreurs d'outil DOIVENT être capturées comme preuves ou incidents. | N2 | post-tool event, incident | QUA-04 | CTRL-OBS-001 |
| AG-TOL-006 | Les hooks DEVRAIENT avoir un cycle shadow/canary/enforced. | N2 | hook registry | GOV-03, GOV-08 | CTRL-PAT-001 |
| AG-TOL-007 | Les surfaces runtime de contrôle DOIVENT avoir owner, statut, mode et preuve. | N4 | runtime surface registry | RUN-02, RUN-08 | CTRL-OBS-001 |
| AG-QUA-001 | Un Done DOIT être appuyé par preuve proportionnée au risque. | N1 | evidence pack | QUA-04 | CTRL-QUA-002 |
| AG-QUA-002 | Les affirmations critiques DOIVENT être reliées à preuve ou hypothèse. | N1 | claim ledger | QUA-01 | CTRL-QUA-001 |
| AG-QUA-003 | Les livrables métier DOIVENT pouvoir être acceptés/refusés par le client. | N1 | dossier d'acceptation | ORG-02 | CTRL-QUA-003 |
| AG-QUA-004 | Les domaines critiques DOIVENT avoir des validateurs identifiés. | N2 | RACI, validation authority | ORG-02, GOV-14 | CTRL-AUT-001 |
| AG-QUA-005 | Les défauts IA plausibles DOIVENT être anticipés. | N2 | registre risques IA | GOV-01 | CTRL-PAT-001 |
| AG-QUA-006 | Les preuves critiques DEVRAIENT être groupées dans un evidence pack. | N1 | evidence pack | QUA-04 | CTRL-QUA-002 |
| AG-QUA-007 | Un verdict DOIT décider fermeture, réouverture, incident ou escalade. | N1 | verification verdict | QUA-04, QUA-05 | CTRL-QUA-003 |
| AG-QUA-008 | Toute transition à risque DOIT être conditionnée par preuve et trigger. | N3 | workflow state manifest, transition event | ORC-09, QUA-05 | CTRL-QUA-003 |
| AG-INC-001 | Une anomalie critique DOIT stopper ou réduire l'autonomie. | N2 | incident containment | GOV-04 | CTRL-INC-001 |
| AG-INC-002 | Tout incident DOIT définir containment, correction, purge mémoire et prévention. | N4 | incident report | KNO-05 | CTRL-INC-001 |
| AG-INC-003 | Les incidents récurrents DOIVENT alimenter evals, hooks ou gouvernance. | N4 | post-mortem, eval update | QUA-13, GOV-03 | CTRL-EVL-001 |
| AG-INC-004 | Les métriques coût, latence, rework, faux Done DEVRAIENT être suivies. | N4 | dashboard, SLO | QUA-08 | CTRL-SLO-001 |
| AG-INC-005 | Toute mémoire contaminée DOIT déclencher invalidation, purge ou correction. | N2 | memory contamination response | KNO-05 | CTRL-RET-001 |
| AG-RET-001 | Tout artefact produit DOIT avoir une destination. | N1 | retention registry | KNO-01, RUN-02 | CTRL-RET-001 |
| AG-RET-002 | Les rapports temporaires NE DEVRAIENT PAS être indexés par défaut. | N1 | retention decision | KNO-01 | CTRL-RET-001 |
| AG-RET-003 | Les sources remplacées DOIVENT pointer vers leur remplacement. | N2 | superseded_by | KNO-08 | CTRL-RET-002 |
| AG-RET-004 | Un nettoyage périodique DOIT vérifier TTL, doublons, obsolescence et données sensibles. | N2 | cleanup report | KNO-01 | CTRL-RET-002 |
| AG-RET-005 | Une mémoire fausse ou contaminée DOIT être purgée et suivie comme incident. | N2 | purge event, incident | KNO-05 | CTRL-INC-001 |
| AG-RET-006 | Les surfaces runtime DOIVENT avoir règle de rétention et statut d'indexation. | N4 | runtime surface registry | RUN-02 | CTRL-RET-002 |
| AG-RET-007 | La dérive docs/manifests/runtime/mémoire DEVRAIT être détectée. | N5 | drift report | KNO-03 | CTRL-PAT-001 |
| AG-RET-008 | Toute promotion en mémoire durable DOIT être justifiée. | N2 | promotion decision | KNO-04 | CTRL-RET-001 |
| AG-DYN-001..005 | Toute capacité dynamique DOIT répondre à un gap, être classée, expirer ou être promue avec preuve. | N4 | capability pack, skill record, lifecycle status | RUN-01, RUN-06, RUN-07 | CTRL-PAT-001 |
| AG-PAT-001..004 | Tout pattern normatif DOIT avoir structure, preuves, maturité et remplacement si déprécié. | N4 | pattern record, maturity matrix | catalogue patterns | CTRL-PAT-001 |
| AG-AUD-001 | Toute conformité déclarée DOIT relier exigence, contrôle, preuve et verdict. | N4 | traceability matrix | audit engine | CTRL-OBS-001 |
| AG-AUD-002 | Toute exception DOIT avoir justification, risque, owner, approbateur, contrôle compensatoire et expiration. | N4 | exception record | audit engine | CTRL-QUA-003 |
| AG-AUD-003 | Une structure gouvernée DOIT maintenir une matrice risques/contrôles/preuves. | N4 | risk-control-evidence matrix | GOV-01 | CTRL-PAT-001 |
| AG-AUD-004 | Un audit DEVRAIT produire niveau atteint, écarts, exceptions et risques résiduels. | N5 | audit report | audit engine | CTRL-PAT-001 |
| AG-OBS-001 | Les runs à risque DOIVENT produire des traces corrélées. | N4 | telemetry events | QUA-08 | CTRL-OBS-001 |
| AG-OBS-002 | Les traces NE DOIVENT PAS exposer secrets ou données inutiles. | N4 | telemetry privacy gate | QUA-08 | CTRL-OBS-002 |
| AG-OBS-003 | Les appels modèle, outil, hook, contexte, preuve et verdict DOIVENT produire une télémétrie suffisante. | N4 | trace completeness report | QUA-08, QUA-10 | CTRL-OBS-003 |
| AG-OBS-004 | Les SLO DEVRAIENT être suivis. | N4 | SLO dashboard, reliability report | QUA-07 | CTRL-SLO-001 |
| AG-OBS-005 | Les événements critiques, incidents et exceptions DOIVENT être conservés selon rétention. | N4 | retention policy, audit log | RUN-02 | CTRL-RET-002 |

## Règle de maintenance

Toute nouvelle exigence AG-* DOIT être ajoutée à cette matrice avant d'être considérée comme normative.

