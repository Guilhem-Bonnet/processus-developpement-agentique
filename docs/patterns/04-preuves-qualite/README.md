# Patterns de preuves et de qualité

Ces patterns transforment les affirmations, transitions et états Done en éléments vérifiables.

La source Mermaid de cette famille est disponible dans [../../../diagrammes/patterns-preuves-qualite.mmd](../../../diagrammes/patterns-preuves-qualite.mmd).

## QUA-01 : Claim ledger

| Élément | Description |
| --- | --- |
| Intention | Transformer les affirmations en éléments vérifiables. |
| Problème | L'agent peut produire des conclusions plausibles mais non prouvées. |
| Solution | Relier chaque affirmation critique à une source, un résultat d'outil ou une hypothèse. |
| Contrôles | QA, critique, dossier d'acceptation, evidence pack. |
| Anti-pattern | Documentation assertive sans provenance. |

## QUA-02 : Observabilité agentique

| Élément | Description |
| --- | --- |
| Intention | Comprendre et améliorer les décisions agentiques. |
| Problème | Sans traces, on ne sait pas pourquoi un agent a agi ni comment corriger. |
| Solution | Capturer prompts, contexte, outils, coûts, latence, erreurs, validations et incidents. |
| Contrôles | Traces, métriques, evals, SLO, post-mortem. |
| Anti-pattern | Système agentique opaque impossible à auditer. |

## QUA-03 : Mission ledger append-only

| Élément | Description |
| --- | --- |
| Intention | Rendre les missions et transitions auditables. |
| Problème | Un état courant écrasé ne permet pas de comprendre pourquoi une décision a changé. |
| Solution | Journaliser missions, tâches, transitions, incidents et preuves comme événements append-only. |
| Contrôles | Machine d'état, actor_id, timestamp, payload, lien evidence/verdict. |
| Anti-pattern | Modifier silencieusement le statut d'une tâche sans événement. |

## QUA-04 : Evidence pack et verification verdict

| Élément | Description |
| --- | --- |
| Intention | Transformer le Done en décision vérifiable. |
| Problème | Les preuves existent mais restent dispersées entre logs, tests, captures et rapports. |
| Solution | Regrouper les preuves dans un evidence pack, puis produire un verdict de vérification. |
| Contrôles | Digest, couverture des critères, profil de preuve, décision close/reopen/incident. |
| Anti-pattern | Fermer une tâche parce qu'un test a été lancé sans relier le résultat aux critères. |

## QUA-05 : Evidence-driven transition

| Élément | Description |
| --- | --- |
| Intention | Autoriser les transitions d'étape seulement par preuves proportionnées au risque. |
| Problème | Une mission peut passer de discovery à cadrage, de dev à QA ou de QA à livraison sans preuve suffisante. |
| Solution | Associer chaque transition à un gate de preuves : critères couverts, risques traités, verdict, prochaine autorité. |
| Contrôles | Pre-stage-transition, evidence pack, verification verdict, DoD d'étape. |
| Anti-pattern | Passer à l'étape suivante parce que le subagent a fini de répondre. |

### Gates typiques

| Transition | Preuve minimale |
| --- | --- |
| Intake -> Discovery | brief, ambiguïtés critiques listées. |
| Discovery -> Cadrage | sources utiles, risques, questions résolues ou escaladées. |
| Cadrage -> Architecture | critères d'acceptation, contraintes, NFR. |
| Architecture -> Implémentation | décision, périmètre, compromis, risques. |
| Implémentation -> QA | diff, tests ou justification, handoff développeur. |
| QA -> Livraison | evidence pack, verdict, risques résiduels. |
| Livraison -> Capitalisation | décision de rétention, mémoire candidate, archive ou purge. |

## QUA-06 : LLM cost registry

| Élément | Description |
| --- | --- |
| Intention | Rendre le coût LLM observable, comparable et gouvernable. |
| Problème | Les coûts tokens sont souvent visibles trop tard dans la facturation provider et difficiles à relier à une mission, un modèle ou un rig. |
| Solution | Maintenir un registre de prix par modèle/provider avec précédence explicite (défauts, pack, projet), puis rattacher tokens, coût estimé et budget à chaque trace. |
| Contrôles | Source de prix, version de pricing, coût par mission, alerte budget, fallback modèle si dépassement. |
| Anti-pattern | Optimiser ou limiter les coûts à partir de factures agrégées sans lien avec les décisions agentiques. |

## QUA-07 : Session reliability SLO reporter

| Élément | Description |
| --- | --- |
| Intention | Mesurer la santé réelle des sessions agentiques par runtime, modèle et version de prompt. |
| Problème | Un agent peut sembler fonctionnel globalement alors qu'un modèle, rig ou prompt version provoque crashs, quarantaines ou idle kills. |
| Solution | Agréger sessions, crashes, quarantaines, idle kills et drain events par Model/PromptVersion/Rig, puis calculer CrashRate% et UnhealthyRate%. |
| Contrôles | SLO de fiabilité, seuil de quarantaine, retrait capacité, incident si dérive persistante. |
| Anti-pattern | Surveiller seulement le succès final sans métriques de santé session. |

## QUA-08 : Agent telemetry plane

| Élément | Description |
| --- | --- |
| Intention | Unifier traces, métriques et événements des agents, modèles, outils, workflows et connaissances. |
| Problème | Les preuves existent mais restent fragmentées entre logs shell, traces provider, prompts, coûts et résultats de test. |
| Solution | Définir un plan télémétrique avec trace_id, mission_id, actor_id, model/provider, tool, state, coût, latence, verdict et incident. |
| Contrôles | OpenTelemetry ou équivalent, corrélation evidence pack, politique de rétention, masquage secrets. |
| Anti-pattern | Collecter des logs bruts impossibles à relier à une décision ou mission. |

## QUA-09 : Prompt/version observability

| Élément | Description |
| --- | --- |
| Intention | Comprendre l'effet des versions de prompts, instructions, skills et modèles. |
| Problème | Un changement de prompt peut dégrader qualité, coût ou sécurité sans être attribuable. |
| Solution | Versionner prompt, instruction, skill, capability pack, provider/model et dataset d'eval dans chaque trace. |
| Contrôles | Prompt registry, eval dataset record, canary, rollback, SLO par version. |
| Anti-pattern | Modifier des instructions partagées sans mesurer impact ni historiser la version. |

## QUA-10 : Trajectory logging

| Élément | Description |
| --- | --- |
| Intention | Rejouer le raisonnement opérationnel observable d'une mission sans exposer de données sensibles inutiles. |
| Problème | Le résultat final ne montre pas quelles sources, outils, validations ou hésitations ont structuré l'action. |
| Solution | Journaliser la trajectoire en événements : intention, contexte chargé, décision, tool call, observation, correction, verdict. |
| Contrôles | Mission ledger, telemetry plane, redaction, evidence pack, retention. |
| Anti-pattern | Garder seulement le transcript brut ou seulement le statut final. |

## QUA-11 : Browser evidence contract

| Élément | Description |
| --- | --- |
| Intention | Rendre les actions UI/browser vérifiables et sûres. |
| Problème | Une validation visuelle ou E2E peut être non reproductible sans DOM, screenshot, console et réseau. |
| Solution | Encadrer URLs, actions autorisées, preuves visuelles, logs et dry-run pour toute interaction navigateur. |
| Contrôles | Browser tool contract, screenshot final, DOM snapshot, console/network logs, blast-radius. |
| Anti-pattern | Cliquer dans une UI de production sans capture, scope ni validation humaine. |

## QUA-12 : Visual Evidence Pack

| Élément | Description |
| --- | --- |
| Intention | Capturer les preuves visuelles nécessaires aux livrables UI, design ou navigateur. |
| Problème | Un test ou une réponse textuelle ne prouve pas toujours l'état réel de l'interface. |
| Solution | Grouper DOM snapshot, screenshots, console, réseau, viewport, parcours et critères UX dans un pack de preuve. |
| Contrôles | Browser tool contract, design validation authority, evidence pack, retention courte. |
| Anti-pattern | Déclarer une interface validée sans capture ni état reproductible. |

## QUA-13 : Eval lifecycle

| Élément | Description |
| --- | --- |
| Intention | Faire évoluer les evals comme un actif de qualité versionné. |
| Problème | Les evals deviennent vite obsolètes si elles ne suivent pas prompts, modèles, skills et incidents. |
| Solution | Versionner datasets, juges, seuils, historique de runs, cas ajoutés depuis incidents et règles de blocage. |
| Contrôles | Eval dataset record, prompt/version observability, canary, rollback. |
| Anti-pattern | Rejouer toujours les mêmes cas sans vérifier qu'ils couvrent les risques actuels. |

## Interfaces liées

| Interface | Rôle |
| --- | --- |
| Claim ledger | Relie affirmation et preuve. |
| Evidence pack | Regroupe les preuves liées aux critères. |
| Verification verdict | Décide fermeture, réouverture, incident ou escalade. |
| Mission ledger | Préserve l'historique des décisions et transitions. |
| Pricing registry | Versionne prix, provider, modèle, unité et précédence. |
| Reliability report | Agrège santé session par modèle, prompt version et rig. |
| Telemetry event schema | Corrèle mission, état, acteur, outil, modèle, coût, preuve et incident. |
| Eval dataset record | Versionne cas, juges, seuils et risques couverts. |
| Browser tool contract | Décrit preuves visuelles, URLs et actions autorisées. |
| Visual evidence pack | Regroupe captures, DOM, logs et critères UX. |
