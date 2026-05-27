# Exigences normatives d'une structure agentique

Cette page exprime les exigences sous forme normative. Elle sert de base de conformité pour vérifier qu'une structure agentique est réellement fonctionnelle, et pas seulement capable de produire du texte.

La table de pilotage qui relie ces exigences aux profils, preuves, patterns et contrôles est la [matrice normative maîtresse](matrice-normative-maitresse.md).

## Mission et besoin

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-MIS-001 | Toute mission DOIT avoir un objectif explicite. | obligatoire |
| AG-MIS-002 | Toute mission DOIT définir périmètre et hors-scope. | obligatoire |
| AG-MIS-003 | Toute mission DOIT posséder des critères d'acceptation vérifiables. | obligatoire |
| AG-MIS-004 | Toute mission DEVRAIT identifier valeur, utilisateurs et contraintes. | recommandé |
| AG-MIS-005 | Toute ambiguïté bloquante DOIT être résolue par contexte vérifié ou question ciblée. | obligatoire |

## Orchestration

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-ORC-001 | Toute tâche non triviale DOIT être représentée par une carte ou un lot traçable. | obligatoire |
| AG-ORC-002 | Toute délégation à un subagent DOIT utiliser un task envelope. | obligatoire |
| AG-ORC-003 | Tout subagent DOIT produire un handoff packet structuré. | obligatoire |
| AG-ORC-004 | L'orchestrateur DOIT limiter le WIP et éviter les délégations ouvertes. | obligatoire |
| AG-ORC-005 | Les communications inter-agents DOIVENT être tracées si elles influencent une décision. | obligatoire |
| AG-ORC-006 | Les transitions de mission ou de tâche DEVRAIENT être journalisées dans un ledger append-only. | recommandé |

## Contexte et mémoire

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-CTX-001 | Le contexte fourni à un agent DOIT être proportionné à son rôle. | obligatoire |
| AG-CTX-002 | Une source critique DOIT avoir provenance, date, statut et propriétaire. | obligatoire |
| AG-CTX-003 | Une base vectorielle DOIT être traitée comme mécanisme de rappel, pas comme vérité. | obligatoire |
| AG-CTX-004 | Le contexte chaud DOIT avoir un TTL et une portée de mission. | obligatoire |
| AG-CTX-005 | Toute source obsolète, remplacée ou sensible DOIT être bloquée ou désindexée. | obligatoire |
| AG-CTX-006 | Une mémoire durable DOIT être stable, sourcée, non sensible ou minimisée. | obligatoire |
| AG-CTX-007 | Une mémoire mature DEVRAIT distinguer rappel vectoriel, graphe relationnel, faits temporels et sources de vérité. | recommandé |
| AG-CTX-008 | Toute lecture mémoire critique DOIT vérifier statut, validité et source active. | obligatoire |
| AG-CTX-009 | Une structure avancée DEVRAIT disposer d'un orchestrateur de contexte qui arbitre profils, budgets, sources, exclusions et persistance. | recommandé |
| AG-CTX-010 | Tout context pack transmis à un subagent DOIT identifier sources incluses, sources exclues, contraintes et niveau de confiance si la tâche est à risque. | obligatoire |
| AG-CTX-011 | Toute contradiction entre sources critiques DOIT être résolue, portée comme hypothèse ou escaladée avant décision durable. | obligatoire |
| AG-CTX-012 | Toute augmentation de budget de contexte DEVRAIT être justifiée par insuffisance, risque ou preuve de contradiction. | recommandé |

## Modèles LLM

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-LLM-001 | Le choix du modèle DOIT dépendre de la tâche, du risque, du coût et de la confidentialité. | obligatoire |
| AG-LLM-002 | Toute tâche à risque DOIT définir un fallback ou une escalade. | obligatoire |
| AG-LLM-003 | Un modèle utilisé pour décision durable DEVRAIT avoir des evals représentatives. | recommandé |
| AG-LLM-004 | Les appels modèle DOIVENT être journalisés au niveau nécessaire : modèle, rôle, coût, latence, erreur. | obligatoire |
| AG-LLM-005 | Les données sensibles NE DOIVENT PAS être transmises à un modèle non autorisé. | obligatoire |
| AG-LLM-006 | Les modèles dépréciés ou interdits DOIVENT déclencher un fallback ou un rejet. | obligatoire |

## Outils et intégrations

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-TOL-001 | Tout outil DOIT être inscrit dans un registre avec risque et permissions. | obligatoire |
| AG-TOL-002 | Toute action destructive, externe ou coûteuse DOIT passer par un hook ou une validation. | obligatoire |
| AG-TOL-003 | Les intégrations MCP DOIVENT définir propriétaire, scopes, timeout et journalisation. | obligatoire |
| AG-TOL-004 | Les secrets NE DOIVENT PAS être exposés dans prompts, logs, traces ou mémoires. | obligatoire |
| AG-TOL-005 | Les erreurs d'outil DOIVENT être capturées comme preuves ou incidents selon gravité. | obligatoire |
| AG-TOL-006 | Les hooks DEVRAIENT avoir un cycle de promotion shadow, canary, enforced ou équivalent. | recommandé |
| AG-TOL-007 | Les surfaces runtime de contrôle DOIVENT avoir propriétaire, statut, mode et preuve de validation. | obligatoire |

## Qualité, preuves et validation

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-QUA-001 | Un état Done DOIT être appuyé par preuve proportionnée au risque. | obligatoire |
| AG-QUA-002 | Les affirmations critiques DOIVENT être reliées à une preuve ou marquées comme hypothèse. | obligatoire |
| AG-QUA-003 | Les livrables métier DOIVENT pouvoir être acceptés ou refusés par le client. | obligatoire |
| AG-QUA-004 | Les domaines sécurité, architecture, UX et ops DOIVENT avoir des validateurs identifiés si concernés. | obligatoire |
| AG-QUA-005 | Les défauts IA plausibles DOIVENT être anticipés sur les cartes non triviales. | obligatoire |
| AG-QUA-006 | Les preuves critiques DEVRAIENT être groupées dans un evidence pack ou équivalent. | recommandé |
| AG-QUA-007 | Un verdict de vérification DOIT décider fermeture, réouverture, incident ou escalade pour les tâches à risque. | obligatoire |
| AG-QUA-008 | Toute transition d'étape à risque DOIT être conditionnée par une preuve proportionnée et un trigger explicite. | obligatoire |

## Incidents et amélioration

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-INC-001 | Une anomalie critique DOIT stopper ou réduire l'autonomie. | obligatoire |
| AG-INC-002 | Tout incident DOIT définir containment, correction, mémoire à purger et prévention. | obligatoire |
| AG-INC-003 | Les incidents récurrents DOIVENT alimenter evals, hooks ou règles de gouvernance. | obligatoire |
| AG-INC-004 | Les métriques de coût, latence, rework, faux Done et validation DEVRAIENT être suivies. | recommandé |
| AG-INC-005 | Toute mémoire contaminée DOIT déclencher invalidation, purge ou correction des sources et caches impactés. | obligatoire |

## Rétention et soutenabilité

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-RET-001 | Tout artefact produit DOIT avoir une destination : durable, archive, TTL, désindexation ou purge. | obligatoire |
| AG-RET-002 | Les rapports temporaires et handoffs NE DEVRAIENT PAS être indexés par défaut. | recommandé |
| AG-RET-003 | Les sources remplacées DOIVENT pointer vers leur remplacement. | obligatoire |
| AG-RET-004 | Un nettoyage périodique DOIT vérifier TTL, doublons, obsolescence et données sensibles. | obligatoire |
| AG-RET-005 | Une mémoire fausse ou contaminée DOIT être purgée et suivie comme incident. | obligatoire |
| AG-RET-006 | Les surfaces de sortie runtime DOIVENT avoir une règle de rétention et un statut d'indexation. | obligatoire |
| AG-RET-007 | La dérive entre documentation, manifests, runtime et mémoire DEVRAIT être détectée périodiquement. | recommandé |
| AG-RET-008 | Toute promotion en mémoire durable DOIT être justifiée par stabilité, source, réutilité, sensibilité, propriétaire et expiration. | obligatoire |

## Capacités dynamiques

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-DYN-001 | Toute création dynamique d'agent, skill, workflow, hook ou instruction DOIT répondre à un gap identifié. | obligatoire |
| AG-DYN-002 | Tout artefact dynamique DOIT être classé éphémère ou permanent. | obligatoire |
| AG-DYN-003 | Un artefact éphémère DOIT avoir une règle d'expiration ou de purge. | obligatoire |
| AG-DYN-004 | La promotion vers durable DOIT être justifiée par usage, valeur et validation. | obligatoire |
| AG-DYN-005 | Les artefacts dynamiques DOIVENT être inscrits dans un registre s'ils influencent l'orchestration. | obligatoire |

## Patterns et maturité

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-PAT-001 | Tout pattern normatif DOIT avoir intention, problème, solution, contrôles et anti-pattern. | obligatoire |
| AG-PAT-002 | Tout pattern normatif DOIT être relié à au moins une exigence et une preuve attendue. | obligatoire |
| AG-PAT-003 | Tout pattern DEVRAIT avoir un statut de lifecycle et un niveau de maturité. | recommandé |
| AG-PAT-004 | Tout pattern déprécié DOIT pointer vers son remplacement ou sa raison de retrait. | obligatoire |

## Audit, observabilité et télémétrie

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-AUD-001 | Toute conformité déclarée DOIT pouvoir être reliée à une exigence, un contrôle, une preuve et un verdict. | obligatoire |
| AG-AUD-002 | Toute exception de conformité DOIT avoir justification, risque, owner, approbateur, contrôle compensatoire et expiration. | obligatoire |
| AG-AUD-003 | Une structure gouvernée DOIT maintenir une matrice risques, contrôles et preuves. | obligatoire |
| AG-AUD-004 | Un audit de conformité DEVRAIT produire un rapport avec niveau atteint, écarts, exceptions et risques résiduels. | recommandé |
| AG-OBS-001 | Les runs agentiques à risque DOIVENT produire des traces corrélées par mission_id, task_id et trace_id. | obligatoire |
| AG-OBS-002 | Les traces, logs et événements NE DOIVENT PAS exposer secrets ou données personnelles inutiles. | obligatoire |
| AG-OBS-003 | Les appels modèle, outil, hook, contexte, preuve et verdict DOIVENT produire une télémétrie suffisante pour audit. | obligatoire |
| AG-OBS-004 | Les SLO agentiques DEVRAIENT être suivis par métriques et alertes. | recommandé |
| AG-OBS-005 | Les événements critiques, incidents et exceptions DOIVENT être conservés selon une politique de rétention explicite. | obligatoire |
