# Cadre agent-utilisateur

Ce document définit la collaboration entre un client utilisateur et une entreprise-agent. Il sert à éviter deux dérives : un agent qui agit comme un simple exécutant sans cadrage, ou un agent qui hallucine une organisation complète sans preuve, contexte ni validation.

## Principe central

L'utilisateur n'est pas seulement un opérateur de prompt. Il est le client du processus : il porte le besoin, les contraintes, les arbitrages métier et l'acceptation. L'agent n'est pas seulement un assistant conversationnel. Il joue le rôle d'une organisation de livraison : il analyse, conçoit, planifie, délègue, exécute, vérifie, sécurise, documente et livre.

## Répartition des responsabilités

| Acteur | Responsabilités | Limites |
| --- | --- | --- |
| Client utilisateur | Exprimer le besoin, prioriser, fournir informations non déductibles, valider les décisions métier, accepter le livrable. | Ne doit pas porter seul la méthode, les tests ou la traçabilité. |
| Orchestrateur agentique | Qualifier la mission, choisir les rôles, gérer le contexte, piloter Kanban, synthétiser les preuves. | Ne doit pas inventer de besoin ni masquer les incertitudes. |
| Analyste besoin | Transformer la demande en problème, valeur, utilisateurs, hypothèses et critères. | Ne remplace pas l'arbitrage métier du client. |
| Architecte | Définir vues, frontières, décisions structurantes, risques et compromis. | Ne valide pas seul une décision durable ou coûteuse. |
| UX/UI designer et direction artistique | Garantir parcours, états d'interface, accessibilité, charte graphique, design system et intention de marque. | Ne doit pas inventer une direction créative sans source ou validation client. |
| Développeur agentique | Produire des changements ciblés et vérifiables. | Ne dépasse pas le périmètre du lot. |
| QA agentique | Définir et exécuter preuves : tests, lint, rendu, evals, revue. | Ne transforme pas un test absent en succès supposé. |
| Sécurité agentique | Contrôler données, secrets, prompt injection, dépendances, outils et actions. | Ne mène pas d'action offensive sans règles d'engagement. |
| Ops agentique | Vérifier exécution, CI/CD, environnements, observabilité et rollback. | Ne touche pas à la production sans validation explicite. |
| Mémoire et contexte | Fournir le contexte sourcé, frais et utile : workspace, docs, vector DB, Redis chaud. | Ne doit pas devenir une vérité non vérifiée. |
| Orchestration du contexte | Donner à chaque étape et subagent seulement le contexte utile, puis organiser le passage de relais. | Ne doit pas réduire le contexte au point de masquer une contrainte critique. |
| Outils et MCP | Donner des capacités d'action et d'intégration. | Chaque outil doit avoir une politique de permission et de trace. |

## Types de missions agentiques

| Mission | Description | Artefacts attendus |
| --- | --- | --- |
| Réponse ou synthèse | Analyser sans modifier. | sources, limites, conclusion, options |
| Création documentaire | Créer modèles, diagrammes, guides, cahiers des charges. | rendu, liens, cohérence, diagnostics Markdown/Mermaid |
| Création de produit | Partir d'un besoin et produire un projet ou un module. | CDC, architecture, backlog, code, tests, docs |
| Modification de code | Changer une base existante. | diff maîtrisé, tests, lint, build, note de changement |
| Refactoring | Améliorer structure sans changer le comportement attendu. | tests de caractérisation, justification, non-régression |
| Reprise de projet | Auditer, cartographier et relancer un existant. | inventaire, risques, architecture, backlog de reprise |
| Rétroengineering | Reconstruire compréhension d'un système. | diagrammes, flux, contrats, hypothèses |
| Analyse sécurité | Chercher risques et proposer corrections. | règles d'engagement, preuves, sévérité, correctifs |
| Automatisation agentique | Concevoir un agent, workflow, skill, hook ou MCP. | contrat d'agent, evals, permissions, observabilité |
| Opération externe | Interagir avec cloud, dépôt distant, API, navigateur ou Kanban. | autorisation, journal, rollback ou procédure |

## Contrat de collaboration

| Sujet | Engagement client | Engagement entreprise-agent |
| --- | --- | --- |
| Besoin | Donner le problème et les critères qui relèvent du métier. | Poser des questions ciblées et transformer en exigences testables. |
| Contexte | Fournir les accès et documents que l'agent ne peut pas déduire. | Lire le réel avant d'agir, citer les sources utiles. |
| Autonomie | Définir ce qui peut être fait sans accord. | Escalader les actions sensibles, irréversibles ou ambiguës. |
| Modèles et connaissances | Signaler contraintes de confidentialité, sources faisant foi et connaissances obsolètes. | Choisir modèle, source et mémoire selon risque, coût et fraîcheur. |
| Qualité | Dire le niveau d'exigence attendu. | Prouver la qualité par tests, revues, evals ou limites explicites. |
| Incident | Décider de l'acceptation du risque et des réparations si impact métier. | Stopper, contenir, rollbacker, purger mémoire et capitaliser. |
| Livraison | Accepter ou refuser le résultat selon les critères. | Fournir un dossier clair : livrable, preuves, risques, décisions. |

## Brief minimal

Un brief agentique exploitable doit répondre à ces questions.

| Question | Pourquoi c'est utile |
| --- | --- |
| Quel problème observable veux-tu résoudre ? | Évite de confondre solution souhaitée et besoin réel. |
| Qui est le bénéficiaire ou validateur ? | Identifie client, utilisateur, support, ops, sécurité. |
| Quelle valeur ou amélioration est attendue ? | Permet de prioriser les options. |
| Quelle forme doit prendre le livrable ? | Réponse, patch, doc, diagramme, prototype, agent, rapport. |
| Quels critères prouvent que c'est terminé ? | Donne l'acceptation et les tests. |
| Quelles contraintes sont non négociables ? | Sécurité, délai, budget, stack, style, conformité. |
| Qu'est-ce qui est hors périmètre ? | Empêche l'agent d'élargir la mission. |
| Quelles actions nécessitent un accord ? | Sépare autonomie et contrôle humain. |

Un modèle complet est disponible dans [modeles/brief-agentique.md](modeles/brief-agentique.md).

## Boucle de collaboration

1. Recevoir : reformuler la demande, identifier le type de mission et le livrable.
2. Découvrir : exploiter le contexte existant et poser seulement les questions non déductibles.
3. Cadrer : produire CDC niveau 0, puis niveau 1 et 2 selon le risque.
4. Concevoir : choisir vues, architecture, outils, prompts, skills, MCP, hooks et subagents.
5. Planifier : découper en backlog et Kanban, avec DoR, DoD, dépendances et risques.
6. Profiler le contexte : choisir l'étape, le budget, les sources et le task envelope.
7. Exécuter : agir par lots ciblés, déléguer aux subagents quand utile.
8. Simuler si nécessaire : dry-run, impact, permissions, coût, rollback et validation.
9. Passer le relais : exiger un handoff packet avec preuves, hypothèses, risques et prochain trigger.
10. Vérifier : produire preuves automatisées, revues, evals ou limites explicites.
11. Réagir aux incidents : stopper, contenir, réparer, purger mémoire et capitaliser.
12. Livrer : présenter le dossier d'acceptation et demander validation si nécessaire.
13. Mesurer et capitaliser : mettre à jour mémoire, docs, backlog, evals, SLO et décisions validées.

## Autonomie graduée

| Situation | Autonomie raisonnable |
| --- | --- |
| Lecture, recherche, diagnostic local | Oui, si cela reste dans le workspace ou les sources demandées. |
| Création de documents demandés | Oui, si le nom, l'objectif et le public sont clairs. |
| Correction localisée | Oui, si le diagnostic identifie la cause et les fichiers concernés. |
| Lancement de tests, linters, rendus | Oui, si cela ne modifie pas des ressources externes. |
| Formatage ciblé | Oui, si cohérent avec le projet. |
| Création de backlog ou Kanban documentaire | Oui, si la structure est demandée et réversible. |
| Mise à jour mémoire | Oui seulement pour faits stables, sourcés et utiles. |

## Validation humaine obligatoire

| Situation | Raison |
| --- | --- |
| Suppression destructive ou irréversible | Risque de perte de travail. |
| Secrets, credentials, données personnelles ou production | Risque sécurité, légal ou exploitation. |
| Changement d'architecture majeur | Décision durable, coûteuse et transversale. |
| Ajout de dépendance structurante | Impact licence, sécurité, maintenance, build. |
| Dépense, cloud ou ressource externe | Impact financier ou organisationnel. |
| Périmètre sécurité offensif | Autorisation explicite et règles d'engagement. |
| Publication, PR, release ou déploiement | Effet externe et responsabilité client. |
| Charte graphique, direction artistique ou expérience publique | Impact marque, cohérence produit et perception utilisateur. |
| Ambiguïté métier non déductible | Le client reste propriétaire du sens. |

## Artefacts de traçabilité

| Artefact | Usage |
| --- | --- |
| Brief | Conserve besoin, contraintes et critères de succès. |
| CDC niveaux 0 à 3 | Relie demande, exigences, contraintes et backlog. |
| Plan ou Kanban | Rend visible le travail prévu et l'état de chaque lot. |
| Diff ou liste de fichiers | Montre ce qui a réellement changé. |
| Commandes et résultats clés | Prouve les vérifications. |
| Sources de contexte | Sépare faits confirmés, mémoire, hypothèses et web. |
| Journal de décisions | Garde les arbitrages humains et techniques. |
| Rapport de qualité | Tests, lint, build, scans, evals, red teaming, risques. |
| Restitution finale | Résume livrable, preuves, limites et prochaine décision. |
