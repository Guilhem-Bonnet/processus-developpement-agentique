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

## Pattern 13 : Mission ledger append-only

| Élément | Description |
| --- | --- |
| Intention | Rendre les missions et transitions auditables. |
| Problème | Un état courant écrasé ne permet pas de comprendre pourquoi une décision a changé. |
| Solution | Journaliser missions, tâches, transitions, incidents et preuves comme événements append-only. |
| Contrôles | machine d'état, actor_id, timestamp, payload, lien evidence/verdict. |
| Anti-pattern | Modifier silencieusement le statut d'une tâche sans événement. |

## Pattern 14 : Evidence pack et verification verdict

| Élément | Description |
| --- | --- |
| Intention | Transformer le Done en décision vérifiable. |
| Problème | Les preuves existent mais restent dispersées entre logs, tests, captures et rapports. |
| Solution | Regrouper les preuves dans un evidence pack, puis produire un verdict de vérification. |
| Contrôles | digest, couverture des critères, profil de preuve, décision close/reopen/incident. |
| Anti-pattern | Fermer une tâche parce qu'un test a été lancé sans relier le résultat aux critères. |

## Pattern 15 : Hook lifecycle progressif

| Élément | Description |
| --- | --- |
| Intention | Déployer les garde-fous sans casser le flux de travail. |
| Problème | Un hook nouveau peut bloquer trop large ou manquer des cas critiques. |
| Solution | Promouvoir les hooks par modes `shadow`, `canary`, puis `enforced`. |
| Contrôles | registre des hooks, digest de validation, faux positifs, procédure de retrait. |
| Anti-pattern | Activer un blocage global sans période d'observation. |

## Pattern 16 : Dynamic factory contrôlée

| Élément | Description |
| --- | --- |
| Intention | Créer de nouvelles capacités sans prolifération incontrôlée. |
| Problème | Agents, skills et workflows dynamiques peuvent devenir une dette invisible. |
| Solution | Détecter le gap, classer l'artefact, décider éphémère/permanent, valider puis promouvoir ou purger. |
| Contrôles | usage tracking, expiration, score de durabilité, review, registre. |
| Anti-pattern | Créer un agent permanent pour chaque demande ponctuelle. |

## Pattern 17 : Mémoire hybride

| Élément | Description |
| --- | --- |
| Intention | Combiner rappel sémantique, relations et faits temporels. |
| Problème | Une vector DB seule rappelle des textes similaires sans comprendre validité ni dépendances. |
| Solution | Associer vectoriel, graphe, sidecar structuré, journal et sources de vérité. |
| Contrôles | source registry, memory gate, valid_from/valid_to, désindexation. |
| Anti-pattern | Traiter le résultat vectoriel comme une vérité. |

## Pattern 18 : Runtime output governance

| Élément | Description |
| --- | --- |
| Intention | Gouverner les artefacts produits par le runtime agentique. |
| Problème | Plans, traces, rapports, captures et sorties temporaires s'accumulent sans statut. |
| Solution | Déclarer type, propriétaire, sensibilité, rétention, indexation et statut. |
| Contrôles | registre de surfaces runtime, cleanup, doc drift, audit périodique. |
| Anti-pattern | Laisser les sorties runtime devenir une documentation parallèle non fiable. |

## Pattern 19 : Doc drift detector

| Élément | Description |
| --- | --- |
| Intention | Empêcher la divergence entre documentation, manifests, hooks, workflows et mémoire. |
| Problème | Le runtime évolue plus vite que le standard documentaire, ou inversement. |
| Solution | Comparer surfaces déclarées, fichiers réels, registres, sources actives et preuves de workflow. |
| Contrôles | hook doc-drift-check, release gate, rapport de drift, owner de correction. |
| Anti-pattern | Considérer la documentation comme vraie sans vérifier le runtime. |

## Pattern 20 : Model retirement guard

| Élément | Description |
| --- | --- |
| Intention | Retirer ou restreindre un modèle sans casser l'orchestration. |
| Problème | Un modèle obsolète peut rester utilisé par habitude ou fallback implicite. |
| Solution | Maintenir statuts active, restricted, deprecated, disallowed et local_only avec fallback explicite. |
| Contrôles | policy de routage, pre-model-route, eval de remplacement, journal d'appel. |
| Anti-pattern | Laisser un modèle interdit accessible parce qu'il fonctionne encore. |
