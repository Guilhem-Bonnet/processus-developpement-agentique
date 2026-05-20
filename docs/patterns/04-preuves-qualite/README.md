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

## Interfaces liées

| Interface | Rôle |
| --- | --- |
| Claim ledger | Relie affirmation et preuve. |
| Evidence pack | Regroupe les preuves liées aux critères. |
| Verification verdict | Décide fermeture, réouverture, incident ou escalade. |
| Mission ledger | Préserve l'historique des décisions et transitions. |
