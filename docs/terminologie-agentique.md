# Terminologie agentique

Cette page définit le vocabulaire minimal d'une structure agentique fonctionnelle. Les termes doivent être utilisés de façon stable dans les autres documents afin d'éviter les ambiguïtés entre conversation, orchestration, mémoire, outil et validation.

## Langage normatif

| Terme | Sens |
| --- | --- |
| DOIT | Exigence obligatoire pour être conforme au standard. |
| DEVRAIT | Recommandation forte, sauf justification explicite. |
| PEUT | Option autorisée selon contexte. |
| NE DOIT PAS | Interdiction ou condition bloquante. |
| CONFORME | Respecte les exigences du profil déclaré. |
| NON CONFORME | Ne respecte pas une exigence obligatoire du profil déclaré. |

## Acteurs

| Terme | Définition |
| --- | --- |
| Client utilisateur | Personne ou organisation qui exprime le besoin, arbitre les priorités et accepte le livrable. |
| Entreprise-agent | Structure agentique qui prend en charge cadrage, exécution, qualité, sécurité, livraison et capitalisation. |
| Orchestrateur | Agent ou composant qui qualifie la mission, découpe le travail, délègue et synthétise les résultats. |
| Subagent | Agent spécialisé recevant un mandat limité, un contexte minimal et une sortie attendue. |
| Validateur | Acteur humain ou agentique autorisé à accepter, bloquer ou escalader une décision dans son domaine. |
| Knowledge janitor | Rôle chargé de l'hygiène documentaire, de la rétention, de l'archivage, de la désindexation et de la purge. |

## Objets de travail

| Terme | Définition |
| --- | --- |
| Mission | Demande qualifiée qui possède objectif, périmètre, risques, critères et propriétaire. |
| Carte Kanban agentique | Unité de pilotage contenant tâche, contexte, droits, modèle, risques, preuves et validation. |
| Task envelope | Contrat de délégation transmis à un subagent : objectif, rôle, contexte, outils, contraintes, sortie. |
| Handoff packet | Paquet de relais produit par un agent : résultat, preuves, hypothèses, risques et prochain déclencheur. |
| Claim ledger | Registre reliant les affirmations importantes à une preuve, une source ou une hypothèse explicite. |
| Dossier d'acceptation | Ensemble de preuves, limites et décisions permettant au client d'accepter ou refuser un livrable. |

## Contexte et mémoire

| Terme | Définition |
| --- | --- |
| Contexte immédiat | Informations présentes dans la conversation ou la fenêtre active. |
| Contexte chaud | État court de mission, souvent stocké en cache ou Redis avec TTL. |
| Contexte long terme | Connaissances récupérables par mémoire, base vectorielle ou documentation indexée. |
| Source de vérité | Artefact actuel faisant foi pour une décision : fichier, test, contrat, décision client, document validé. |
| Mémoire durable | Fait stable, sourcé, non sensible et utile à plusieurs missions futures. |
| Source obsolète | Source remplacée, expirée ou non fiable qui ne doit plus guider une décision. |
| Désindexation | Retrait d'une source de la recherche vectorielle sans nécessairement supprimer l'artefact original. |

## Capacités agentiques

| Terme | Définition |
| --- | --- |
| Prompt registry | Registre des instructions stables par rôle, versionnées et contrôlées. |
| Skills registry | Registre de procédures réutilisables activables dans des conditions définies. |
| Tool registry | Inventaire des outils disponibles, permissions, risques et limites. |
| MCP gateway | Passerelle standardisée vers des outils, données ou workflows externes. |
| Hook | Point de contrôle interceptant une action avant ou après une étape critique. |
| Policy engine | Composant qui décide autorisation, blocage ou escalade selon règles, risques et permissions. |
| Model router | Composant qui choisit le modèle ou LLM selon tâche, risque, coût, confidentialité et evals. |

## Qualité et sûreté

| Terme | Définition |
| --- | --- |
| Eval | Cas de test agentique permettant de mesurer un prompt, un modèle, un subagent ou un workflow. |
| SLO agentique | Objectif mesurable de qualité, coût, latence, sécurité, rework ou fiabilité. |
| Dry-run | Simulation contrôlée d'une action risquée avant exécution réelle. |
| Incident agentique | Erreur significative impliquant action non autorisée, faux Done, mémoire polluée, fuite ou mauvaise décision. |
| Faux Done | État où l'agent annonce une tâche terminée sans preuve suffisante. |
| Mémoire polluée | Mémoire contenant fait faux, obsolète, sensible ou non sourcé. |
