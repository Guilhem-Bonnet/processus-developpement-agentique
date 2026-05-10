# Modèle de brief agentique

Ce modèle aide le client utilisateur à formuler une demande exploitable par une entreprise-agent. Il peut être rempli complètement pour une mission sensible ou partiellement pour une tâche simple. Les champs vides doivent être soit complétés, soit explicitement marqués comme non applicables.

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Nom de la mission | A renseigner |
| Date | A renseigner |
| Client demandeur | A renseigner |
| Validateur final | A renseigner |
| Agent, équipe agentique ou mode utilisé | A renseigner |
| Workspace, dépôt ou environnement | A renseigner |
| Statut | brouillon / cadrage / prêt / en cours / vérification / livré / bloqué |
| Niveau de risque | faible / moyen / élevé / critique |
| Défauts IA plausibles | hallucination / surconfiance / oubli / complaisance / faux Done / mémoire polluée / autre |
| SLO ou métrique de succès | A renseigner |

## 1. Besoin client

| Question | Réponse |
| --- | --- |
| Quel problème observable veux-tu résoudre ? | A renseigner |
| Pourquoi maintenant ? | A renseigner |
| Qui est concerné ? | client / utilisateur final / support / ops / sécurité / métier / autre |
| Quelle valeur attendue ? | A renseigner |
| Quelle situation future prouverait que c'est réussi ? | A renseigner |
| Quelle forme doit prendre le livrable ? | réponse / patch / doc / diagramme / rapport / prototype / projet / agent / autre |

## 2. Objectif et type de mission

| Élément | Description |
| --- | --- |
| Type de mission | création / évolution / correction / refactoring / reprise / sécurité / agent IA / opération externe / autre |
| Objectif principal | A renseigner |
| Objectifs secondaires | A renseigner |
| Hors périmètre | A renseigner |
| Décisions attendues du client | A renseigner |

## 3. Cahier des charges synthétique

| Niveau | Contenu |
| --- | --- |
| Niveau 0 : cadrage | problème, valeur, parties prenantes, scope, hors-scope, risques |
| Niveau 1 : comportement | fonctionnalités, parcours, règles métier, critères d'acceptation |
| Niveau 2 : contraintes | sécurité, accessibilité, performance, données, ops, fiabilité IA |
| Niveau 3 : exécution | backlog, tâches, tests, DoR, DoD, dépendances, priorités |

## 4. Périmètre opérationnel

| Élément | Description |
| --- | --- |
| Inclus | A renseigner |
| Exclu | A renseigner |
| Fichiers ou dossiers concernés | A renseigner |
| Systèmes externes concernés | A renseigner |
| Données sensibles ou réglementées | A renseigner |
| Contraintes de style ou méthode | A renseigner |
| Charte graphique, design system ou DA | A renseigner |
| Contraintes de délai, coût ou environnement | A renseigner |

## 5. Contexte et mémoire

| Source | Usage autorisé | Conditions |
| --- | --- | --- |
| Workspace local | oui / non | A renseigner |
| Documentation projet | oui / non | A renseigner |
| Historique git ou PR | oui / non | A renseigner |
| Tickets, Kanban, backlog | oui / non | A renseigner |
| Web et références officielles | oui / non | A renseigner |
| Base vectorielle | oui / non | sources, métadonnées, seuils, réindexation |
| Redis contexte chaud | oui / non | TTL, séparation mission, invalidation |
| Mémoire persistante agent | oui / non | faits stables, sourcés, non sensibles |
| Budget de contexte par défaut | tiny / small / medium / deep | selon étape et risque |
| Modèle IA préféré ou imposé | oui / non | modèle, raison, confidentialité, fallback |
| Politique de routage LLM | oui / non | modèle par tâche, budget, fallback, evals |
| Sources interdites | oui / non | données sensibles, domaines, dossiers, tickets |
| Politique de rétention/nettoyage | oui / non | durable, archive, TTL, désindexation, purge |

## 6. Permissions outils

| Action | Autorisée ? | Conditions |
| --- | --- | --- |
| Lire le workspace | oui / non | A renseigner |
| Modifier des fichiers | oui / non | périmètre et validation diff |
| Lancer tests, lint, build | oui / non | commandes autorisées |
| Installer des dépendances | oui / non | justification, licence, sécurité |
| Accéder au réseau | oui / non | domaines ou sources autorisés |
| Utiliser navigateur ou rendu visuel | oui / non | A renseigner |
| Utiliser MCP | oui / non | serveurs, scopes, logs |
| Interagir avec dépôt distant | oui / non | branche, PR, review, validation |
| Modifier Kanban ou tickets | oui / non | projet, colonnes, règles |
| Toucher à la production | non par défaut | validation explicite obligatoire |
| Manipuler secrets ou données sensibles | non par défaut | procédure dédiée obligatoire |

## 7. Orchestration agentique

| Élément | Décision |
| --- | --- |
| Prompts ou instructions spécifiques | A renseigner |
| Prompts de rôle à utiliser | orchestrateur / analyste / architecte / dev / UX / UI / DA / QA / sécurité / ops / doc / mémoire |
| Skills à utiliser ou créer | A renseigner |
| Subagents nécessaires | analyste / architecte / dev / UX / UI / DA / QA / sécurité / ops / doc / autre |
| Profil de contexte | intake / discovery / cadrage / architecture / implémentation / QA / sécurité / livraison / capitalisation |
| Budget tokens/contexte | tiny / small / medium / deep, avec règle d'escalade |
| Routage LLM par tâche | modèle principal / fallback / justification |
| Dry-run requis | oui / non, conditions |
| Claim ledger attendu | oui / non, affirmations à sourcer |
| Critique anti-défauts IA | non / checklist / subagent critique / revue humaine |
| Task envelope attendu | mission / contexte minimal / outils / critères / sortie |
| Handoff packet attendu | résumé / preuves / hypothèses / risques / prochain trigger |
| Consultation inter-agent | autorisée / interdite / soumise à validation, agents concernés |
| Hooks obligatoires | pre-context-load / pre-delegation / pre-tool / post-tool / pre-write / pre-memory-write / pre-stage-transition / pre-release / stop |
| Niveau d'autonomie | lecture seule / édition locale / outils externes / livraison assistée |
| Mode de validation | automatique / revue subagent / revue humaine / mixte |

## 8. Backlog et Kanban

| Champ | Valeur |
| --- | --- |
| Épopée ou thème | A renseigner |
| Lots principaux | A renseigner |
| Cartes à créer | A renseigner |
| Dépendances | A renseigner |
| Critères Definition of Ready | A renseigner |
| Critères Definition of Done | A renseigner |
| Limite WIP | A renseigner |
| Validateur par carte | A renseigner |
| Accès et permissions par carte | A renseigner |
| SLO ou métriques par carte | A renseigner |
| Procédure incident / rollback | A renseigner |
| Rétention des artefacts | mémoire durable / archive / TTL / purge / désindexation |
| Blocages connus | A renseigner |

## 9. Critères de succès et preuves

| Critère | Preuve attendue |
| --- | --- |
| Le livrable répond au besoin | critères d'acceptation validés |
| Le comportement attendu est couvert | tests, scénarios, exemples ou revue |
| Les changements restent dans le périmètre | diff ou liste de fichiers |
| Les contraintes qualité sont respectées | ISO 25010, sécurité, accessibilité, performance selon contexte |
| Les risques IA sont maîtrisés | evals, red teaming, contrôle contexte, limites documentées |
| Le contexte est maîtrisé | profil, budget, sources et handoff packet documentés |
| Les outils et actions sont tracés | journal de mission, commandes et résultats clés |
| La documentation utile est à jour | fichiers ou sections concernés |
| Les risques restants sont connus | synthèse finale et décisions ouvertes |

## 10. Validation humaine attendue

| Point de décision | Validateur | Quand |
| --- | --- | --- |
| Besoin et scope initial | A renseigner | avant réalisation |
| Architecture ou dépendance structurante | A renseigner | avant implémentation |
| Action risquée ou externe | A renseigner | avant exécution |
| Résultat de sécurité | A renseigner | avant livraison |
| Acceptation finale | A renseigner | fin de mission |

## 11. Journal de mission

| Étape | Action | Preuve | Décision |
| --- | --- | --- | --- |
| 1 | A renseigner | A renseigner | A renseigner |

## 12. Restitution attendue

La réponse finale de l'entreprise-agent doit contenir :

- le besoin traité ;
- le livrable produit ;
- les fichiers, diagrammes, cartes ou artefacts concernés ;
- les outils, MCP, subagents ou sources importants utilisés ;
- les vérifications effectuées ;
- les limites, tests absents ou risques restants ;
- les décisions encore nécessaires, s'il y en a ;
- les éléments à capitaliser en mémoire, documentation ou backlog.
