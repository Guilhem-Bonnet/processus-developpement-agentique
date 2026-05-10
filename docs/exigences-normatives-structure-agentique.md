# Exigences normatives d'une structure agentique

Cette page exprime les exigences sous forme normative. Elle sert de base de conformité pour vérifier qu'une structure agentique est réellement fonctionnelle, et pas seulement capable de produire du texte.

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

## Contexte et mémoire

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-CTX-001 | Le contexte fourni à un agent DOIT être proportionné à son rôle. | obligatoire |
| AG-CTX-002 | Une source critique DOIT avoir provenance, date, statut et propriétaire. | obligatoire |
| AG-CTX-003 | Une base vectorielle DOIT être traitée comme mécanisme de rappel, pas comme vérité. | obligatoire |
| AG-CTX-004 | Le contexte chaud DOIT avoir un TTL et une portée de mission. | obligatoire |
| AG-CTX-005 | Toute source obsolète, remplacée ou sensible DOIT être bloquée ou désindexée. | obligatoire |
| AG-CTX-006 | Une mémoire durable DOIT être stable, sourcée, non sensible ou minimisée. | obligatoire |

## Modèles LLM

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-LLM-001 | Le choix du modèle DOIT dépendre de la tâche, du risque, du coût et de la confidentialité. | obligatoire |
| AG-LLM-002 | Toute tâche à risque DOIT définir un fallback ou une escalade. | obligatoire |
| AG-LLM-003 | Un modèle utilisé pour décision durable DEVRAIT avoir des evals représentatives. | recommandé |
| AG-LLM-004 | Les appels modèle DOIVENT être journalisés au niveau nécessaire : modèle, rôle, coût, latence, erreur. | obligatoire |
| AG-LLM-005 | Les données sensibles NE DOIVENT PAS être transmises à un modèle non autorisé. | obligatoire |

## Outils et intégrations

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-TOL-001 | Tout outil DOIT être inscrit dans un registre avec risque et permissions. | obligatoire |
| AG-TOL-002 | Toute action destructive, externe ou coûteuse DOIT passer par un hook ou une validation. | obligatoire |
| AG-TOL-003 | Les intégrations MCP DOIVENT définir propriétaire, scopes, timeout et journalisation. | obligatoire |
| AG-TOL-004 | Les secrets NE DOIVENT PAS être exposés dans prompts, logs, traces ou mémoires. | obligatoire |
| AG-TOL-005 | Les erreurs d'outil DOIVENT être capturées comme preuves ou incidents selon gravité. | obligatoire |

## Qualité, preuves et validation

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-QUA-001 | Un état Done DOIT être appuyé par preuve proportionnée au risque. | obligatoire |
| AG-QUA-002 | Les affirmations critiques DOIVENT être reliées à une preuve ou marquées comme hypothèse. | obligatoire |
| AG-QUA-003 | Les livrables métier DOIVENT pouvoir être acceptés ou refusés par le client. | obligatoire |
| AG-QUA-004 | Les domaines sécurité, architecture, UX et ops DOIVENT avoir des validateurs identifiés si concernés. | obligatoire |
| AG-QUA-005 | Les défauts IA plausibles DOIVENT être anticipés sur les cartes non triviales. | obligatoire |

## Incidents et amélioration

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-INC-001 | Une anomalie critique DOIT stopper ou réduire l'autonomie. | obligatoire |
| AG-INC-002 | Tout incident DOIT définir containment, correction, mémoire à purger et prévention. | obligatoire |
| AG-INC-003 | Les incidents récurrents DOIVENT alimenter evals, hooks ou règles de gouvernance. | obligatoire |
| AG-INC-004 | Les métriques de coût, latence, rework, faux Done et validation DEVRAIENT être suivies. | recommandé |

## Rétention et soutenabilité

| ID | Exigence | Niveau |
| --- | --- | --- |
| AG-RET-001 | Tout artefact produit DOIT avoir une destination : durable, archive, TTL, désindexation ou purge. | obligatoire |
| AG-RET-002 | Les rapports temporaires et handoffs NE DEVRAIENT PAS être indexés par défaut. | recommandé |
| AG-RET-003 | Les sources remplacées DOIVENT pointer vers leur remplacement. | obligatoire |
| AG-RET-004 | Un nettoyage périodique DOIT vérifier TTL, doublons, obsolescence et données sensibles. | obligatoire |
| AG-RET-005 | Une mémoire fausse ou contaminée DOIT être purgée et suivie comme incident. | obligatoire |
