# Questionnaires agentiques

Ce document sert à cadrer une mission où l'utilisateur agit comme client et l'agent comme entreprise. Il reprend la profondeur du processus humain, puis ajoute les dimensions agentiques : contexte, mémoire, outils, prompts, skills, MCP, hooks, subagents, Kanban, qualité IA et validation.

## Règle d'usage

L'agent ne doit pas poser toutes ces questions au client à chaque mission. Il doit d'abord exploiter ce qui est disponible : brief, workspace, README, tickets, erreurs, historique, documentation, références officielles, mémoire validée, Kanban. Il ne pose ensuite que les questions dont la réponse n'est pas déductible et dont l'absence crée un risque réel.

## 1. Identifier l'objectif du travail

| Objectif | Questions clés | Livrables attendus |
| --- | --- | --- |
| Création de produit | Quel problème résout-on ? Pour qui ? Quelle valeur attendue ? Quel MVP ? | vision, CDC niveau 0, backlog initial |
| Évolution ou correction | Quel comportement doit changer ? Quelle régression éviter ? Quel impact utilisateur ? | diagnostic, critères d'acceptation, patch ou plan |
| Refactoring | Quelle qualité améliore-t-on ? Quel comportement doit rester stable ? | audit, tests de caractérisation, ADR si besoin |
| Reprise de projet | Que sait-on de l'existant ? Quelles zones sont critiques ? | inventaire, cartographie, risques, backlog de reprise |
| Analyse sécurité | Quel périmètre est autorisé ? Quels assets ? Quelles limites ? | règles d'engagement, matrice risques, rapport |
| Automatisation agentique | Quel travail veut-on déléguer à un agent ? Quelle autonomie ? | contrat d'agent, outils, permissions, evals |
| Agent RAG ou mémoire | Quelles sources ? Quelle fraîcheur ? Quel risque de mauvaise récupération ? | stratégie d'indexation, vector DB, Redis chaud, tests |
| Opération externe | Quel système externe ? Quel coût ou impact ? Quel rollback ? | autorisation, procédure, journal, plan de reprise |
| Documentation | Quel public ? Quelle décision le document doit-il aider ? | structure, références, diagrammes, validation |

## 2. Définir le besoin client

### Concepts utiles

| Concept | Quand l'utiliser | Sortie attendue |
| --- | --- | --- |
| 5W2H / QQOQCCP | Besoin flou ou incomplet. | qui, quoi, où, quand, comment, combien, pourquoi |
| 5 Why | Problème symptomatique ou demande de solution prématurée. | cause racine probable, hypothèses à vérifier |
| Double Diamond | Projet important avec découverte et convergence. | découverte, définition, développement, livraison |
| Personas | Interface ou produit utilisé par plusieurs profils. | profils, objectifs, contraintes, niveau d'expertise |
| Parcours utilisateur | Processus ou UI avec étapes. | étapes, points de friction, opportunités |
| Impact mapping | Besoin de prioriser par valeur. | objectifs, acteurs, impacts, options |
| Event storming | Domaine métier riche ou backend complexe. | événements, commandes, règles, agrégats |
| Threat modeling | Sécurité, données sensibles ou agents outillés. | menaces, actifs, contrôles, risques résiduels |

### Questions de besoin

- Quel problème observable veut-on résoudre ?
- Qui est le client final, l'utilisateur final, le validateur, l'exploitant, le support ?
- Quelle situation actuelle pose problème ?
- Quelle situation future serait considérée comme réussie ?
- Quelle valeur métier, technique ou opérationnelle est attendue ?
- Quels objectifs sont mesurables ?
- Quels éléments sont explicitement hors périmètre ?
- Quelles contraintes sont déjà connues : délai, budget, stack, sécurité, données, conformité, dette, disponibilité ?
- Quelles hypothèses doivent être validées avant d'investir davantage ?
- Quel niveau d'autonomie peut être donné à l'entreprise-agent ?

## 3. Construire le cahier des charges agentique

| Niveau | Questions | Livrables |
| --- | --- | --- |
| Niveau 0 : cadrage | Pourquoi ? Pour qui ? Quelle valeur ? Quels risques ? Quelle autonomie ? | vision, objectifs, scope, hors-scope, parties prenantes, risques |
| Niveau 1 : comportement | Que doit faire le produit ou l'agent ? Quels parcours ? Quelles règles ? | user stories, critères d'acceptation, exemples, erreurs attendues |
| Niveau 2 : contraintes | Quelles qualités et limites ? Sécurité ? Données ? Performance ? Ops ? Risques IA ? | NFR, contrôles sécurité, exigences données, SLO, evals, garde-fous |
| Niveau 3 : exécution | Comment découper, vérifier et livrer ? | backlog Kanban, tâches, tests, DoR, DoD, dépendances, permissions |

## 4. Questionnement frontend et UX

| Axe | Questions à poser |
| --- | --- |
| Utilisateurs | Qui utilise l'interface ? Quel niveau d'expertise ? Quels besoins d'assistance ? |
| Parcours | Quelles tâches principales ? Quelles étapes critiques ? Quels retours arrière ? |
| États UI | Chargement, vide, erreur, succès, conflit, non autorisé, partiel ? |
| Accessibilité | Cible WCAG ? Navigation clavier ? Focus visible ? Contrastes ? Alternatives ? |
| Contenus | Quelle hiérarchie ? Quels libellés métier ? Quels messages d'erreur ? |
| Design system | Quelle charte graphique, quels tokens, composants, maquettes ou captures font foi ? |
| Direction artistique | Quelle marque, quel ton, quelle ambiance, quelles références validées ? |
| Données | Données personnelles ? Consentement ? Export ? Suppression ? Rétention ? |
| Validation | Wireframes, prototype, capture, test E2E ou audit accessibilité ? |
| Agent UI | L'interface expose-t-elle les actions de l'agent, son statut, ses limites et demandes d'accord ? |

## 5. Questionnement backend, données et intégrations

| Axe | Questions à poser |
| --- | --- |
| Domaine | Quels concepts métier ? Quelles règles et invariants ? |
| API | REST, GraphQL, RPC, événements ? OpenAPI ? Versioning ? |
| Données | Modèle, volumétrie, cohérence, migration, archivage, suppression ? |
| Authentification | Sessions, tokens, OAuth/OIDC, MFA, rotation ? |
| Autorisation | Rôles, permissions, scopes, tenants, séparation de données ? |
| Intégrations | Services tiers, webhooks, files, batchs, idempotence, retries ? |
| Observabilité | Logs, métriques, traces, audit trail, alertes ? |
| Résilience | Timeouts, circuit breaker, rollback, backup, restore ? |
| Sécurité | Validation entrées, secrets hors code, chiffrement, OWASP ASVS ? |
| Agentique | Quels outils externes peuvent être appelés par l'agent via MCP ou API ? |

## 6. Context engineering

| Sujet | Questions |
| --- | --- |
| Sources de vérité | Quels fichiers, docs, tickets, CI, logs ou contrats font foi ? |
| Mémoire longue | Quelles connaissances doivent être indexées en base vectorielle ? |
| Mémoire chaude | Quel état de session doit vivre dans Redis : tâche en cours, cache, files, événements ? |
| Gouvernance connaissance | Qui possède la source ? Quelle version, date, sensibilité et durée de vie ? |
| Rétention | Quels rapports, handoffs, logs ou traces doivent expirer, être archivés, désindexés ou purgés ? |
| Source active | Quelle version fait foi si plusieurs documents se contredisent ? |
| Métadonnées | Quels filtres : projet, version, date, propriétaire, sensibilité, type de document ? |
| Qualité de récupération | Quel top-k ? Quels seuils de similarité ? Quelle stratégie si les résultats divergent ? |
| Budget de contexte | Quel volume est nécessaire pour cette étape : tiny, small, medium, deep ? |
| Profil par étape | Intake, discovery, architecture, implémentation, QA, sécurité, livraison ou capitalisation ? |
| Fraîcheur | Quand réindexer ? Quand invalider Redis ? Quand ignorer une mémoire périmée ? |
| Sécurité | Quelles données ne doivent jamais être indexées, mémorisées ou exposées ? |
| Preuve | Comment relier chaque réponse agentique à une source ou un résultat d'outil ? |

## 7. Prompts, skills, outils et MCP

| Élément | Questions |
| --- | --- |
| Instructions | Quelles règles stables guident l'entreprise-agent ? |
| Prompts de mission | Quel format de demande réduit les ambiguïtés ? |
| Skills | Quelles procédures réutilisables faut-il : audit, test, sécurité, documentation, release ? |
| Outils locaux | Lecture, édition, terminal, navigateur, rendu, tests : lesquels sont autorisés ? |
| MCP | Quels systèmes externes doivent être connectés : GitHub, Figma, DB, tickets, cloud, docs ? |
| Permissions | Quels outils sont lecture seule ? Quels outils peuvent modifier ? Quels outils exigent accord ? |
| Validation | Qui valide métier, design, sécurité, ops, QA et acceptation finale ? |
| Économie de tokens | Quel budget par étape ? Quelles règles de cache, compression et escalade ? |
| Routage modèle | Quel modèle par rôle ? Quel fallback ? Quelles contraintes coût, latence, confidentialité ? |
| Évaluation modèle | Quels cas prouvent que ce modèle est adapté à ce rôle ? |
| Sandboxing | Les commandes peuvent-elles s'exécuter en environnement isolé ? |
| Journal | Quelles actions doivent être tracées pour audit ou acceptation ? |

## 8. Hooks et garde-fous

| Moment | Questions |
| --- | --- |
| Avant action | Le besoin, le périmètre et la preuve attendue sont-ils clairs ? |
| Avant contexte | Le budget, les sources et les seuils de récupération sont-ils définis ? |
| Après contexte | Les sources récupérées sont-elles fraîches, pertinentes et non sensibles ? |
| Avant outil | L'outil est-il autorisé ? Les paramètres sont-ils sûrs ? |
| Après outil | Le résultat est-il exploitable ? Contient-il secret, erreur ou contradiction ? |
| Avant écriture | Le fichier est-il dans le périmètre ? Le changement est-il réversible ? |
| Avant livraison | DoD atteinte ? Tests passés ? Risques critiques fermés ? |
| Fin de tâche | Que capitaliser ? Que ne pas mémoriser ? Que dire au client ? |
| Passage d'étape | Le handoff packet est-il complet et le prochain trigger clair ? |
| Avant modèle | Le modèle choisi est-il autorisé pour ces données, ce coût et ce risque ? |
| Avant réutilisation contexte | La source est-elle active, fraîche, non remplacée et indexable ? |
| Nettoyage périodique | Quelle cadence pour nettoyer Redis, vector DB, rapports temporaires et handoffs ? |
| Avant dry-run | L'action risquée a-t-elle un plan, un impact, un rollback et une validation ? |
| Incident | Que faire si un faux Done, une fuite, une régression ou une action non autorisée est détectée ? |

## 9. Subagents

| Besoin | Subagent possible | Questions de délégation |
| --- | --- | --- |
| Recherche volumineuse | Explore / analyste | Que doit-il lire ? Quel résumé suffit ? |
| Architecture | architecte | Quelles décisions et contraintes doit-il comparer ? |
| Implémentation | développeur | Quel lot précis ? Quels fichiers ? Quels tests ? |
| Vérification | QA | Quels tests, rendus, evals ou diagnostics ? |
| Sécurité | sécurité | Quels actifs, menaces, secrets, dépendances ? |
| Design UI/UX ou DA | designer | Quelle charte, quels composants, quels parcours, quelle intention visuelle ? |
| Livraison | ops | Quel build, CI, déploiement, rollback, observabilité ? |
| Documentation | documentation | Quel public, format, références et liens ? |

### Contrat de subagent

| Élément | Question |
| --- | --- |
| Task envelope | Quelle mission, quel contexte minimal, quels outils et quelle sortie ? |
| Budget | Quelle taille de contexte maximale pour ce rôle ? |
| Handoff packet | Quelles preuves, hypothèses, risques et prochain trigger doivent revenir ? |
| Mémoire | Que peut-on écrire, invalider ou oublier après la tâche ? |
| Consultation | Quels autres agents peuvent être consultés et avec quel contexte minimal ? |

## 10. Kanban et pilotage

| Niveau | Questions |
| --- | --- |
| Backlog | Quelles demandes, risques, bugs, dettes et décisions sont visibles ? |
| Priorité | Quelle valeur, urgence, risque ou dépendance justifie l'ordre ? |
| DoR | La tâche est-elle assez claire pour l'agent et vérifiable ? |
| WIP | Combien de lots en parallèle sans perdre la maîtrise ? |
| Blocages | Qu'est-ce qui demande une réponse client, un accès, une décision ou un test ? |
| Accès | Quels scopes, outils, MCP ou systèmes externes sont autorisés pour cette carte ? |
| Validation | Qui ferme la carte : QA, sécurité, design, ops, client ou mixte ? |
| Dry-run | Quelles cartes nécessitent simulation avant exécution ? |
| Incident | Quelle procédure de rollback ou reprise s'applique ? |
| DoD | Quelles preuves ferment la carte ? |
| Capitalisation | Quelles décisions rejoignent docs, mémoire, evals ou backlog ? |

## 11. Qualité, fiabilité et acceptation

| Famille | Questions |
| --- | --- |
| Tests | Unitaires, intégration, contrat, E2E, accessibilité, performance, migration ? |
| Evals IA | Quels cas représentatifs pour juger l'agent ou le prompt ? |
| Red teaming | Quelles attaques : prompt injection, données sensibles, outil excessif, jailbreak ? |
| Défauts IA | Quels risques : hallucination, surconfiance, oubli, complaisance, faux Done, mémoire polluée ? |
| Claim ledger | Quelles affirmations devront être reliées à une preuve ? |
| Critique | Faut-il une simple checklist, un subagent critique ou une revue humaine ? |
| SLO | Quels seuils : acceptation premier passage, faux Done, coût, latence, rework ? |
| Observabilité | Quelles traces, métriques, logs et scorecards doivent être conservés ? |
| Modèles | Quel modèle est évalué, versionné, autorisé ou interdit ? |
| Revue | Faut-il une revue croisée par subagent, humain ou CI ? |
| Observabilité | Quelles traces, métriques et logs prouvent le comportement ? |
| Risques résiduels | Quels tests impossibles, hypothèses, limites ou dettes restent ouverts ? |
| Acceptation client | Quelles preuves le client doit-il voir pour accepter ? |

## 12. Restitution finale

La restitution doit répondre clairement aux points suivants.

- Quel besoin a été traité ?
- Quel livrable a été produit ?
- Quels fichiers, outils, subagents ou sources ont été utilisés ?
- Quelles vérifications prouvent le résultat ?
- Quels risques, limites ou tests absents restent ouverts ?
- Quelle décision client est encore nécessaire, le cas échéant ?
- Quels SLO, incidents, coûts ou apprentissages doivent être suivis après livraison ?
