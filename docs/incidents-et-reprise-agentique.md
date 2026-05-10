# Incidents et reprise agentique

Un système agentique doit prévoir l'échec. L'objectif n'est pas de promettre qu'un agent ne cassera jamais rien, mais de détecter vite, limiter l'impact, corriger proprement et améliorer les garde-fous.

## Types d'incidents

| Incident | Exemple | Gravité possible |
| --- | --- | --- |
| Faux Done | tâche marquée terminée sans preuve réelle. | moyenne à critique |
| Mauvais patch | régression, fichier hors périmètre, config cassée. | moyenne à critique |
| Fuite de données | secret affiché, mémoire polluée, log sensible. | élevée à critique |
| Action externe non autorisée | PR, ticket, cloud, production sans accord. | élevée à critique |
| Prompt injection réussie | contenu non fiable devient instruction. | élevée |
| Mémoire fausse | fait erroné réutilisé par un autre run. | moyenne |
| Coût incontrôlé | boucle outil, contexte trop large, modèle profond abusif. | faible à élevée |
| Incident design | livraison incohérente avec charte ou accessibilité. | faible à moyenne |
| Incident sécurité | dépendance vulnérable, scope trop large, scan ignoré. | élevée |

## Sévérité

| Niveau | Définition | Réponse |
| --- | --- | --- |
| Faible | impact local, réversible, pas de donnée sensible. | corriger et journaliser. |
| Moyen | rework significatif ou validation erronée. | bloquer carte, revue critique, correction. |
| Élevé | impact externe, sécurité, données, architecture ou client. | incident formel, rollback, validation humaine. |
| Critique | production, secret, perte de données, effet légal ou financier. | arrêt immédiat, escalade, post-mortem. |

## Processus de réponse

1. Détecter : hook, test, client, QA, sécurité, observabilité ou critique.
2. Stopper : arrêter l'action, suspendre la carte, bloquer les outils risqués.
3. Contenir : isoler fichiers, secrets, mémoire, caches, tickets ou environnements touchés.
4. Diagnostiquer : identifier cause racine, contexte utilisé, outil appelé, décision fautive.
5. Réparer : rollback, patch, purge mémoire, rotation secret, correction doc ou ticket.
6. Vérifier : tests, scan, revue, eval anti-régression.
7. Capitaliser : post-mortem, garde-fou, eval, prompt, skill ou template mis à jour.

## Rollback par surface

| Surface | Stratégie |
| --- | --- |
| Fichiers locaux | diff inverse ciblé, sauvegarde, patch de correction. |
| Git | revert commit ou PR correctrice, jamais reset destructif sans accord. |
| Mémoire Redis | suppression clé, TTL court, invalidation mission. |
| Base vectorielle | supprimer points, réindexer sources valides, marquer version obsolète. |
| Kanban | rouvrir carte, ajouter incident, lier post-mortem. |
| MCP externe | annuler action si API le permet, notifier propriétaire. |
| Production | procédure runbook, rollback versionné, validation ops obligatoire. |
| Secrets | rotation, révocation, audit d'exposition. |

## Post-mortem agentique

| Rubrique | Question |
| --- | --- |
| Résumé | Que s'est-il passé ? |
| Impact | Qui ou quoi a été affecté ? |
| Détection | Comment l'incident a-t-il été découvert ? |
| Cause racine | Quel défaut process, contexte, outil, prompt ou modèle ? |
| Défaut IA | hallucination, oubli, surconfiance, faux Done, mémoire polluée ? |
| Garde-fou manquant | Quel hook, eval ou validation aurait bloqué ? |
| Réparation | Qu'est-ce qui a été corrigé ou rollbacké ? |
| Prévention | Quel changement dans prompt, skill, test, eval, mémoire ou Kanban ? |
| Propriétaire | Qui suit la correction durable ? |

## Critères de clôture

Un incident agentique n'est fermé que si :

- l'impact est compris et documenté ;
- le livrable ou l'état touché est réparé ou explicitement accepté ;
- la mémoire et les caches contaminés sont corrigés ou invalidés ;
- une preuve de correction existe ;
- le garde-fou manquant est ajouté au backlog ou implémenté ;
- le client ou propriétaire concerné est informé si nécessaire.

## Règle finale

Un incident non capitalisé est une dette de gouvernance. Chaque erreur agentique doit améliorer le système qui l'a rendue possible.
