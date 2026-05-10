# Patterns de structure agentique

Cette page décrit les patterns structurants d'une organisation agentique. Chaque pattern exprime un problème récurrent, une solution stable et les contrôles nécessaires pour qu'il fonctionne en production documentaire ou opérationnelle.

## Pattern 1 : Entreprise-agent

| Élément | Description |
| --- | --- |
| Intention | Traiter l'agent comme une organisation opératrice plutôt que comme un simple assistant. |
| Problème | Un agent conversationnel mélange besoin, exécution, validation et mémoire. |
| Solution | Séparer rôles, responsabilités, validations, preuves et mémoire comme dans une entreprise. |
| Contrôles | RACI, Kanban, validateur final, contrats entre rôles, dossier d'acceptation. |
| Anti-pattern | Agent unique qui décide, exécute et valide seul. |

## Pattern 2 : Orchestrateur et subagents spécialisés

| Élément | Description |
| --- | --- |
| Intention | Déléguer sans perdre le contrôle. |
| Problème | Un agent généraliste sature en contexte et oublie les contraintes. |
| Solution | L'orchestrateur découpe le travail et transmet des task envelopes à des subagents spécialisés. |
| Contrôles | WIP limité, outils par rôle, handoff packet, revue croisée. |
| Anti-pattern | Subagents autonomes qui explorent librement sans contrat de sortie. |

## Pattern 3 : Task envelope

| Élément | Description |
| --- | --- |
| Intention | Donner à un agent exactement ce qu'il doit faire. |
| Problème | Les prompts longs et flous produisent dérive, coûts et faux Done. |
| Solution | Encapsuler mission, rôle, contexte minimal, outils, contraintes, critères et format de sortie. |
| Contrôles | Pre-delegation, budget de contexte, policy engine. |
| Anti-pattern | Coller tout l'historique de conversation à chaque agent. |

## Pattern 4 : Handoff packet

| Élément | Description |
| --- | --- |
| Intention | Passer le relais sans recharger toute la mission. |
| Problème | Les étapes suivantes perdent les décisions ou héritent de bruit inutile. |
| Solution | Résumer résultat, preuves, hypothèses, risques, changements et prochain déclencheur. |
| Contrôles | Post-subagent, claim ledger, journal de preuves. |
| Anti-pattern | Rapport narratif long sans action suivante ni preuve. |

## Pattern 5 : Context router

| Élément | Description |
| --- | --- |
| Intention | Fournir un contexte utile, frais et proportionné. |
| Problème | Trop peu de contexte crée hallucination ; trop de contexte crée confusion. |
| Solution | Sélectionner sources par rôle, étape, risque, budget et fraîcheur. |
| Contrôles | Pre-context-load, Post-context-load, Pre-context-reuse. |
| Anti-pattern | RAG large sans filtres ni métadonnées. |

## Pattern 6 : Model router

| Élément | Description |
| --- | --- |
| Intention | Utiliser le bon modèle pour la bonne tâche. |
| Problème | Le modèle par défaut peut être trop faible, trop cher ou non autorisé. |
| Solution | Router selon tâche, rôle, risque, confidentialité, coût, modalité et evals. |
| Contrôles | Pre-model-route, fallback, evals, logs coût/latence. |
| Anti-pattern | Choix implicite du modèle pour toutes les tâches. |

## Pattern 7 : Policy engine et hooks

| Élément | Description |
| --- | --- |
| Intention | Prévenir les actions non autorisées avant qu'elles se produisent. |
| Problème | Les agents peuvent appeler outils, écrire, pousser ou supprimer au mauvais moment. |
| Solution | Intercepter les moments critiques avec règles allow/block/escalate. |
| Contrôles | Pre-tool, Pre-write, Pre-release, Pre-dry-run, Incident-detected. |
| Anti-pattern | Revue seulement après exécution. |

## Pattern 8 : Claim ledger

| Élément | Description |
| --- | --- |
| Intention | Transformer les affirmations en éléments vérifiables. |
| Problème | L'agent peut produire des conclusions plausibles mais non prouvées. |
| Solution | Relier chaque affirmation critique à une source, un résultat d'outil ou une hypothèse. |
| Contrôles | QA, critique, dossier d'acceptation. |
| Anti-pattern | Documentation assertive sans provenance. |

## Pattern 9 : Knowledge janitor

| Élément | Description |
| --- | --- |
| Intention | Empêcher la mémoire et les documents de devenir toxiques ou ingouvernables. |
| Problème | Les vieux rapports, traces et décisions remplacées polluent le contexte futur. |
| Solution | Classer artefacts en durable, archive, TTL, désindexation ou purge. |
| Contrôles | Pre-index, Scheduled-cleanup, registre de rétention. |
| Anti-pattern | Tout indexer parce que tout pourrait servir un jour. |

## Pattern 10 : Dry-run avant action risquée

| Élément | Description |
| --- | --- |
| Intention | Simuler avant d'agir sur un système externe, coûteux ou irréversible. |
| Problème | Un agent peut produire un changement correct localement mais dangereux en contexte réel. |
| Solution | Décrire impact, permissions, coût, rollback, validation et critères de go/no-go. |
| Contrôles | Pre-dry-run, validation humaine, rollback. |
| Anti-pattern | Déploiement, suppression ou appel externe sans simulation. |

## Pattern 11 : Validation authority

| Élément | Description |
| --- | --- |
| Intention | Savoir qui peut accepter ou bloquer. |
| Problème | L'agent confond complétion technique et acceptation métier. |
| Solution | Définir les autorités par domaine : client, QA, sécurité, ops, design, architecture. |
| Contrôles | RACI, matrice de validation, dossier d'acceptation. |
| Anti-pattern | L'agent ferme une carte sensible sans validateur. |

## Pattern 12 : Observabilité agentique

| Élément | Description |
| --- | --- |
| Intention | Comprendre et améliorer les décisions agentiques. |
| Problème | Sans traces, on ne sait pas pourquoi un agent a agi ni comment corriger. |
| Solution | Capturer prompts, contexte, outils, coûts, latence, erreurs, validations et incidents. |
| Contrôles | traces, métriques, evals, SLO, post-mortem. |
| Anti-pattern | Système agentique opaque impossible à auditer. |
