# Matrice de maturité des patterns

Cette matrice indique à partir de quel profil un pattern devient attendu. Elle ne remplace pas les exigences normatives : elle sert à éviter une adoption trop lourde au démarrage.

## Profils

| Profil | Sens |
| --- | --- |
| Minimal | Le système peut cadrer, déléguer et prouver une tâche simple. |
| Contrôlé | Le système limite outils, risques, sources et permissions. |
| Orchestré | Le système coordonne plusieurs agents, sources, modèles et transitions. |
| Gouverné | Le système mesure qualité, coûts, incidents, evals et lifecycle. |
| Production | Le système agit dans des environnements sensibles, multi-tenant ou infra. |

## Matrice synthétique

| Pattern | Profil d'entrée | Pourquoi |
| --- | --- | --- |
| ORG-01 Entreprise-agent | Minimal | relation client / entreprise-agent. |
| ORG-02 Validation authority | Minimal | acceptation et arbitrage humain. |
| ORC-01 Orchestrateur et subagents | Orchestré | coordination multi-rôles. |
| ORC-02 Task envelope | Minimal | délégation bornée. |
| ORC-03 Handoff packet | Minimal | passage de relais. |
| ORC-04 Context router | Orchestré | sélection de sources. |
| ORC-05 Orchestrateur de contexte avancé | Gouverné | arbitrage complet sources/mémoire/budget. |
| ORC-06 Context constitution | Contrôlé | ordre d'autorité des sources. |
| ORC-07 Context conflict resolver | Contrôlé | contradiction avant décision durable. |
| ORC-08 Context budget escalation | Contrôlé | coût et contexte proportionnés. |
| ORC-09 Workflow State Engine | Orchestré | états et reprises explicites. |
| ORC-10 Flow DSL minimal | Gouverné | flows réutilisables et exportables. |
| GOV-01 Policy engine et hooks | Minimal | décision allow/block/escalate. |
| GOV-02 Dry-run avant action risquée | Contrôlé | simulation avant effet externe. |
| GOV-03 Hook lifecycle progressif | Contrôlé | shadow/canary/enforced. |
| GOV-04 Autonomie gouvernée | Minimal | autonomie proportionnée au risque. |
| GOV-05 Agent privilege boundary | Production | séparation controller/agent. |
| GOV-06 Merge lane fault classifier | Gouverné | retries non aveugles. |
| GOV-07 Tool blast-radius limiter | Minimal | limiter impact des outils. |
| GOV-08 Guardrail contract | Contrôlé | garde-fous versionnés. |
| GOV-09 MCP Trust Gate | Contrôlé | intégrations MCP qualifiées. |
| GOV-10 Policy by environment | Production | local/staging/prod séparés. |
| GOV-11 Cluster action dry-run | Production | action infra simulée. |
| GOV-12 Prompt Injection Firewall | Contrôlé | contenu externe non fiable. |
| GOV-13 Remote Hygiene Guard | Gouverné | sources distantes fraîches et auditées. |
| GOV-14 Decision Council Gate | Gouverné | quorum pour décisions critiques. |
| QUA-01 Claim ledger | Minimal | preuves des affirmations. |
| QUA-02 Observabilité agentique | Gouverné | traces, métriques et audit. |
| QUA-03 Mission ledger append-only | Orchestré | historique causal. |
| QUA-04 Evidence pack et verification verdict | Minimal | Done prouvé. |
| QUA-05 Evidence-driven transition | Orchestré | transitions conditionnées. |
| QUA-06 LLM cost registry | Gouverné | coût relié aux traces. |
| QUA-07 Session reliability SLO reporter | Production | santé des sessions. |
| QUA-08 Agent telemetry plane | Gouverné | plan télémétrique unifié. |
| QUA-09 Prompt/version observability | Gouverné | régressions attribuables. |
| QUA-10 Trajectory logging | Gouverné | trajectoire rejouable. |
| QUA-11 Browser evidence contract | Orchestré | preuve navigateur. |
| QUA-12 Visual Evidence Pack | Orchestré | captures et rendu UX. |
| QUA-13 Eval lifecycle | Gouverné | evals versionnées et rejouables. |
| KNO-01 Knowledge janitor | Minimal | éviter accumulation. |
| KNO-02 Mémoire hybride | Orchestré | rappel, graphe et source. |
| KNO-03 Doc drift detector | Gouverné | docs/runtime alignés. |
| KNO-04 Knowledge promotion | Minimal | capitalisation contrôlée. |
| KNO-05 Memory contamination response | Contrôlé | purge/correction mémoire. |
| KNO-06 Knowledge Base Indexer | Minimal | corpus externe gouverné. |
| KNO-07 Memory integrity validator | Contrôlé | audit mémoire. |
| KNO-08 Doc-to-graph pipeline | Gouverné | relations sourcées. |
| KNO-09 Knowledge narrative packaging | Gouverné | synthèse sourcée. |
| KNO-10 Source Graph Resolver | Gouverné | résolution graph/source. |
| MOD-01 Model router | Orchestré | choix modèle par tâche. |
| MOD-02 Model retirement guard | Gouverné | retrait/fallback modèle. |
| RUN-01 Dynamic factory contrôlée | Gouverné | création dynamique maîtrisée. |
| RUN-02 Runtime output governance | Minimal | artefacts runtime gouvernés. |
| RUN-03 Kubernetes agent control plane | Production | exécution cluster. |
| RUN-04 Orders exec/formula dispatcher | Orchestré | shell vs workflow agentique. |
| RUN-05 Primitive-first capability model | Orchestré | rôles configurables. |
| RUN-06 Capability marketplace | Orchestré | packs découvrables. |
| RUN-07 Skill/capability lifecycle | Gouverné | promotion/retrait. |
| RUN-08 Runtime provider contract | Gouverné | backend interchangeable. |
| RUN-09 Agent backend boundary | Orchestré | ports/adapters. |
| RUN-10 Local agent worker pool | Production | workers et queue. |
| RUN-11 Workspace isolation | Production | workspace, secrets, réseau. |
| RUN-12 Secure Local Coordinator | Production | coordination locale sans proxy de tokens. |

