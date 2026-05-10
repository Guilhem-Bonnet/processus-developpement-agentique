# Contrats opérationnels agentiques

Cette page rassemble les contrats d'interface entre les étapes, les agents, les outils et le client. Le but est de rendre l'entreprise-agent composable : chaque rôle sait ce qu'il reçoit, ce qu'il produit et qui peut valider.

## Contrats principaux

| Contrat | Producteur | Consommateur | Usage |
| --- | --- | --- | --- |
| Brief agentique | client / orchestrateur | analyste, orchestrateur | démarrer une mission. |
| Carte Kanban agentique | orchestrateur | subagents, client, QA | piloter un lot. |
| Task envelope | orchestrateur | subagent | déléguer sans bruit. |
| Handoff packet | subagent | orchestrateur, étape suivante | passer le relais. |
| Claim ledger | producteur / QA | critique, client, livraison | prouver les affirmations. |
| Registre risques IA | orchestrateur | critique, QA, sécurité | anticiper défauts IA. |
| Contrat MCP | ops / sécurité | orchestrateur, outils | gouverner intégrations externes. |
| Dossier d'acceptation | orchestrateur | client | livrer et faire accepter. |
| Rapport d'incident | détecteur / orchestrateur | client, sécurité, ops | réparer et capitaliser. |
| Fiche subagent | propriétaire agentique | orchestrateur | versionner rôle, outils et limites. |

## Templates disponibles

- [Brief agentique](modeles/brief-agentique.md)
- [Carte Kanban agentique](modeles/carte-kanban-agentique.md)
- [Claim ledger](modeles/claim-ledger.md)
- [Registre des risques IA](modeles/registre-risques-ia.md)
- [Dossier d'acceptation](modeles/dossier-acceptation.md)
- [Rapport d'incident agentique](modeles/incident-agentique.md)
- [Contrat MCP](modeles/contrat-mcp.md)
- [Fiche subagent](modeles/fiche-subagent.md)
- [Politique de routage LLM](modeles/politique-routage-llm.md)
- [Registre de rétention des connaissances](modeles/registre-retention-connaissances.md)

## Contrat analyste vers architecte

| Entrée analyste | Sortie attendue architecte |
| --- | --- |
| problème, valeur, utilisateurs, scope, contraintes, critères | options, frontières, compromis, risques, ADR éventuel |

## Contrat architecte vers développeur

| Entrée architecte | Sortie attendue développeur |
| --- | --- |
| décision, périmètre, contraintes, fichiers ou modules, risques | patch ciblé, tests, limites, handoff QA |

## Contrat design vers développeur

| Entrée design | Sortie attendue développeur |
| --- | --- |
| parcours, états UI, charte, design system, critères visuels | implémentation cohérente, captures ou rendu, limites |

## Contrat développeur vers QA

| Entrée développeur | Sortie attendue QA |
| --- | --- |
| diff, critères, tests lancés, risques, hypothèses | rapport de validation, défauts, go/no-go |

## Contrat sécurité vers release

| Entrée sécurité | Sortie attendue livraison |
| --- | --- |
| risques, sévérité, corrections, acceptations, exceptions | décision go/no-go, risques résiduels, suivi |

## Contrat ops vers livraison

| Entrée ops | Sortie attendue livraison |
| --- | --- |
| build, CI, configuration, rollback, observabilité | runbook, statut déploiement, alertes, limites |

## Contrat critique vers orchestrateur

| Entrée critique | Sortie attendue orchestrateur |
| --- | --- |
| sortie agent, claim ledger, critères, contexte | défauts plausibles, preuves faibles, questions, go/no-go |

## Règle finale

Un agent peut improviser dans sa méthode, mais pas dans ses interfaces. Les contrats évitent que la créativité d'un rôle devienne du chaos pour le suivant.
