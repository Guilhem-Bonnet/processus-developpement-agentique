# Contrats opérationnels agentiques

Cette page rassemble les contrats d'interface entre les étapes, les agents, les outils et le client. Le but est de rendre l'entreprise-agent composable : chaque rôle sait ce qu'il reçoit, ce qu'il produit et qui peut valider. Ces contrats opérationnalisent les exigences du [modèle de référence](modele-reference-structure-agentique.md) et des [exigences normatives](exigences-normatives-structure-agentique.md).

## Contrats principaux

| Contrat | Producteur | Consommateur | Usage |
| --- | --- | --- | --- |
| Brief agentique | client / orchestrateur | analyste, orchestrateur | démarrer une mission. |
| Carte Kanban agentique | orchestrateur | subagents, client, QA | piloter un lot. |
| Context pack | orchestrateur de contexte | subagents, QA, sécurité | transmettre un contexte vérifié et limité. |
| Knowledge source index | owner source / ops / documentation | knowledge base indexer, orchestrateur de contexte | greffer un corpus externe indexable avec connecteur, ACL, fraîcheur et réindexation. |
| Workflow state manifest | architecte / orchestrateur | workflow engine, audit | déclarer états, transitions, guards, interruptions et preuves. |
| Task envelope | orchestrateur | subagent | déléguer sans bruit. |
| Handoff packet | subagent | orchestrateur, étape suivante | passer le relais. |
| Claim ledger | producteur / QA | critique, client, livraison | prouver les affirmations. |
| Evidence pack | QA / outil / orchestrateur | validateur, client, livraison | regrouper les preuves. |
| Verification verdict | validateur / QA | orchestrateur, Kanban, client | décider fermeture, réouverture ou incident. |
| Mission ledger event | orchestrateur / runtime | audit, mémoire, observabilité | tracer transitions et décisions. |
| Registre des surfaces runtime | orchestrateur / ops | gouvernance, sécurité, mémoire | gouverner prompts, hooks, skills, traces et artefacts. |
| Registre risques IA | orchestrateur | critique, QA, sécurité | anticiper défauts IA. |
| Pattern record | architecte / gouvernance | référentiel agentique | suivre statut, maturité, exigences et preuves d'un pattern. |
| Control record | gouvernance / sécurité / ops | orchestrateur, audit | définir contrôle, trigger, preuve et télémétrie. |
| Exception de conformité | gouvernance / validateur | audit, client, ops | accepter temporairement un écart contrôlé. |
| Événement télémétrique | runtime / orchestrateur | observabilité, audit | corréler traces, métriques, logs et décisions. |
| Pricing registry | runtime / ops | observabilité, model router, audit | versionner coûts LLM par provider/modèle et relier coûts aux missions. |
| Registre des providers LLM | gouvernance modèles / ops | model router, observabilité, audit | déclarer providers, adapters, modèles, capacités, policies, evals et fallback. |
| Reliability report | runtime / observabilité | ops, gouvernance, audit | mesurer santé des sessions par modèle, prompt version et rig. |
| Controller-agent privilege contract | controller / sécurité | runtime provider, policy engine | séparer permissions controller/agent et scrubber tokens avant spawn. |
| Order dispatcher contract | orchestrateur / runtime | policy engine, agents, QA | distinguer exec shell-only et formula workflow agentique avec budget et preuves. |
| Runtime provider contract | ops / runtime | orchestrateur, policy engine | normaliser lifecycle, ressources, logs, santé et cleanup d'un backend d'exécution. |
| Capability pack | owner capacité | orchestrateur, marketplace | déclarer rôles, skills, permissions, tests, version et runtime compatible. |
| Skill record | owner skill | orchestrateur, subagents | décrire activation, inputs, outputs, limites, permissions et preuves. |
| Guardrail contract | sécurité / gouvernance | policy engine, orchestrateur | définir guardrails input/output/tool/model avec décisions et télémétrie. |
| Browser tool contract | QA / design / sécurité | agents UI, policy engine | gouverner URLs, actions navigateur, preuves visuelles et blast-radius. |
| Eval dataset record | QA / observabilité | model router, prompt registry | versionner cas d'évaluation, juges, seuils et dérives. |
| Source graph record | documentation / architecture | context router, audit | tracer nœuds, relations, contradictions et preuves entre sources. |
| Memory routing policy | gouvernance connaissances | context router, memory gate | définir L0-L3, sources de vérité, rappel et promotion mémoire. |
| Flow DSL minimal | architecte / orchestrateur | workflow engine | décrire petits flows exportables avec états et transitions gardées. |
| Rapport d'audit | auditeur / gouvernance | client, direction, équipe agentique | statuer sur conformité, écarts et risques résiduels. |
| Contrat MCP | ops / sécurité | orchestrateur, outils | gouverner intégrations externes. |
| Dossier d'acceptation | orchestrateur | client | livrer et faire accepter. |
| Rapport d'incident | détecteur / orchestrateur | client, sécurité, ops | réparer et capitaliser. |
| Fiche subagent | propriétaire agentique | orchestrateur | versionner rôle, outils et limites. |

## Templates disponibles

- [Brief agentique](modeles/brief-agentique.md)
- [Carte Kanban agentique](modeles/carte-kanban-agentique.md)
- [Context pack](modeles/context-pack.md)
- [Knowledge source index](modeles/knowledge-source-index.md)
- [Workflow state manifest](modeles/workflow-state-manifest.md)
- [Task envelope](modeles/task-envelope.md)
- [Handoff packet](modeles/handoff-packet.md)
- [Claim ledger](modeles/claim-ledger.md)
- [Evidence pack](modeles/evidence-pack.md)
- [Verification verdict](modeles/verification-verdict.md)
- [Memory record](modeles/memory-record.md)
- [Pattern record](modeles/pattern-record.md)
- [Control record](modeles/control-record.md)
- [Exception de conformité](modeles/exception-conformite.md)
- [Événement télémétrique](modeles/telemetry-event.md)
- [Pricing registry](modeles/pricing-registry.md)
- [Registre des providers LLM](modeles/llm-provider-registry.md)
- [Reliability report](modeles/reliability-report.md)
- [Controller-agent privilege contract](modeles/controller-agent-privilege-contract.md)
- [Order dispatcher contract](modeles/order-dispatcher-contract.md)
- [Runtime provider contract](modeles/runtime-provider-contract.md)
- [Capability pack](modeles/capability-pack.md)
- [Skill record](modeles/skill-record.md)
- [Guardrail contract](modeles/guardrail-contract.md)
- [Browser tool contract](modeles/browser-tool-contract.md)
- [Eval dataset record](modeles/eval-dataset-record.md)
- [Source graph record](modeles/source-graph-record.md)
- [Memory routing policy](modeles/memory-routing-policy.md)
- [Flow DSL minimal](modeles/flow-dsl-minimal.md)
- [Rapport d'audit](modeles/audit-report.md)
- [Événement de mission ledger](modeles/mission-ledger-event.md)
- [Registre des surfaces runtime](modeles/registre-surfaces-runtime.md)
- [Matrice de conformité agentique](modeles/matrice-conformite-agentique.md)
- [Registre des risques IA](modeles/registre-risques-ia.md)
- [Dossier d'acceptation](modeles/dossier-acceptation.md)
- [Rapport d'incident agentique](modeles/incident-agentique.md)
- [Contrat MCP](modeles/contrat-mcp.md)
- [Fiche subagent](modeles/fiche-subagent.md)
- [Politique de routage LLM](modeles/politique-routage-llm.md)
- [Registre de rétention des connaissances](modeles/registre-retention-connaissances.md)

## Exemples remplis

- [Workflow feature simple](modeles/exemples/workflow-feature-simple.md)
- [Knowledge source repo produit](modeles/exemples/knowledge-source-repo-produit.md)
- [LLM provider multi-provider](modeles/exemples/llm-provider-multi-provider.md)
- [Capability pack reviewer](modeles/exemples/capability-pack-reviewer.md)
- [Browser tool validation UI](modeles/exemples/browser-tool-validation-ui.md)

## Contrat analyste vers architecte

| Entrée analyste | Sortie attendue architecte |
| --- | --- |
| problème, valeur, utilisateurs, scope, contraintes, critères | options, frontières, compromis, risques, ADR éventuel |

## Contrat orchestrateur de contexte vers subagent

| Entrée orchestrateur de contexte | Sortie attendue subagent |
| --- | --- |
| context pack, task envelope, contraintes, sources incluses/exclues, scorecard | handoff packet sourcé, preuves, hypothèses, risques, prochaine étape |

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
