# Matrice patterns, exigences et preuves

Cette matrice relie les patterns aux exigences normatives et aux preuves attendues. Elle complète la [matrice de preuves de conformité](../matrice-preuves-conformite-agentique.md) en ajoutant la dimension design pattern.

## Matrice synthétique

| Pattern | Exigences couvertes | Preuves attendues |
| --- | --- | --- |
| ORG-01 Entreprise-agent | AG-MIS-001, AG-ORC-001, AG-QUA-003 | brief, Kanban, RACI, dossier d'acceptation. |
| ORG-02 Validation authority | AG-QUA-003, AG-QUA-004, AG-QUA-007 | matrice de validation, verdict, acceptation client. |
| ORC-01 Orchestrateur et subagents | AG-ORC-001, AG-ORC-004, AG-ORC-005 | workflow, trace de délégation, limites WIP. |
| ORC-02 Task envelope | AG-ORC-002, AG-CTX-001, AG-TOL-001 | task envelope, outils autorisés, critères de sortie. |
| ORC-03 Handoff packet | AG-ORC-003, AG-ORC-006, AG-QUA-002 | handoff packet, mission ledger, hypothèses et risques. |
| ORC-04 Context router | AG-CTX-001, AG-CTX-002, AG-CTX-003 | logs de récupération, source registry, filtres de fraîcheur. |
| ORC-05 Orchestrateur de contexte avancé | AG-CTX-009, AG-CTX-010, AG-RET-001 | context pack, scorecard, décision de persistance. |
| ORC-06 Context constitution | AG-CTX-002, AG-CTX-003, AG-CTX-008 | règles de vérité, source registry, politique de conflit. |
| ORC-07 Context conflict resolver | AG-MIS-005, AG-CTX-008, AG-QUA-002 | rapport de contradiction, décision, escalade ou hypothèse. |
| ORC-08 Context budget escalation | AG-CTX-001, AG-LLM-001, AG-LLM-004 | justification budget, logs coût/tokens, validation si dépassement. |
| ORC-09 Workflow State Engine | AG-ORC-001, AG-ORC-006, AG-QUA-008 | workflow state manifest, transition log, interruption record. |
| ORC-10 Flow DSL minimal | AG-ORC-001, AG-PAT-002 | flow DSL minimal, export Mermaid, validation de guards. |
| GOV-01 Policy engine et hooks | AG-TOL-001, AG-TOL-002, AG-TOL-006 | policy manifest, hook registry, décisions allow/block/escalate. |
| GOV-02 Dry-run avant action risquée | AG-TOL-002, AG-INC-001, AG-QUA-007 | dry-run report, rollback plan, go/no-go. |
| GOV-03 Hook lifecycle progressif | AG-TOL-006, AG-INC-003 | mode shadow/canary/enforced, faux positifs, validation. |
| GOV-04 Autonomie gouvernée | AG-QUA-004, AG-TOL-002, AG-INC-001 | niveau d'autonomie, validation authority, blocages. |
| GOV-05 Agent privilege boundary | AG-TOL-004, AG-TOL-007, AG-OBS-003 | controller-agent privilege contract, env scrub event, protected keys audit. |
| GOV-06 Merge lane fault classifier | AG-INC-003, AG-OBS-003 | failure classification, retry budget, escalation record. |
| GOV-07 Tool blast-radius limiter | AG-TOL-001, AG-TOL-002, AG-OBS-003 | policy decision, tool scope, dry-run ou blocage. |
| GOV-08 Guardrail contract | AG-TOL-006, AG-AUD-003, AG-OBS-003 | guardrail contract, mode, décision, métrique faux positifs. |
| GOV-09 MCP Trust Gate | AG-TOL-003, AG-TOL-004, AG-TOL-001 | contrat MCP, scopes, variables, allowlist d'outils. |
| GOV-10 Policy by environment | AG-TOL-001, AG-TOL-002, AG-QUA-004 | environment policy, validation authority, audit prod. |
| GOV-11 Cluster action dry-run | AG-TOL-002, AG-INC-001, AG-AUD-003 | dry-run cluster, impact report, rollback, go/no-go. |
| GOV-12 Prompt Injection Firewall | AG-TOL-004, AG-OBS-003, AG-INC-001 | source trust label, isolation instructions/données, blocage. |
| GOV-13 Remote Hygiene Guard | AG-CTX-002, AG-RET-007, AG-AUD-003 | remote audit, ref freshness, dirty-skip-pull, quarantine. |
| GOV-14 Decision Council Gate | AG-QUA-004, AG-QUA-007, AG-LLM-002 | council record, quorum, veto, dissent log, verdict. |
| MOD-01 Model router | AG-LLM-001, AG-LLM-002, AG-LLM-005 | politique de routage, fallback, journal modèle. |
| MOD-02 Model retirement guard | AG-LLM-006 | statut modèle, fallback cible, eval de remplacement. |
| QUA-01 Claim ledger | AG-QUA-002 | claim ledger, source ou hypothèse liée. |
| QUA-02 Observabilité agentique | AG-LLM-004, AG-INC-004 | traces, métriques, SLO, coûts, latence. |
| QUA-03 Mission ledger append-only | AG-ORC-006 | mission ledger, événements append-only. |
| QUA-04 Evidence pack et verdict | AG-QUA-001, AG-QUA-006, AG-QUA-007 | evidence pack, verification verdict. |
| QUA-05 Evidence-driven transition | AG-ORC-006, AG-QUA-001, AG-QUA-007 | gate de transition, DoD, verdict lié. |
| QUA-06 LLM cost registry | AG-LLM-004, AG-INC-004, AG-OBS-004 | pricing registry, coût par mission, budget alert. |
| QUA-07 Session reliability SLO reporter | AG-OBS-004, AG-INC-004 | reliability report, CrashRate, UnhealthyRate, quarantine. |
| QUA-08 Agent telemetry plane | AG-OBS-001, AG-OBS-002, AG-OBS-003 | telemetry events, trace completeness, redaction report. |
| QUA-09 Prompt/version observability | AG-LLM-003, AG-OBS-003, AG-PAT-003 | prompt version, eval dataset record, canary/rollback. |
| QUA-10 Trajectory logging | AG-ORC-006, AG-OBS-001, AG-AUD-001 | trajectory log, mission ledger events, evidence links. |
| QUA-11 Browser evidence contract | AG-TOL-001, AG-QUA-001, AG-OBS-003 | browser tool contract, DOM snapshot, screenshot, network/console logs. |
| QUA-12 Visual Evidence Pack | AG-QUA-001, AG-QUA-004, AG-OBS-003 | screenshots, DOM, viewport, design criteria, console/network logs. |
| QUA-13 Eval lifecycle | AG-LLM-003, AG-INC-003, AG-OBS-004 | eval dataset record, judge, threshold, run history, blocking decision. |
| KNO-01 Knowledge janitor | AG-RET-001, AG-RET-004 | cleanup report, registre de rétention. |
| KNO-02 Mémoire hybride | AG-CTX-007, AG-CTX-008 | memory audit, graphe, sidecar, source registry. |
| KNO-03 Doc drift detector | AG-RET-007 | rapport de drift, comparaison runtime/docs. |
| KNO-04 Knowledge promotion | AG-CTX-006, AG-RET-001, AG-RET-002 | mémoire candidate, preuve source, décision de promotion. |
| KNO-05 Memory contamination response | AG-INC-002, AG-RET-005 | incident, purge, correction, eval de prévention. |
| KNO-06 Knowledge Base Indexer | AG-CTX-001, AG-CTX-002, AG-CTX-003, AG-RET-001 | knowledge source index, logs d'indexation, ACL, freshness report, résultats sourcés. |
| KNO-07 Memory integrity validator | AG-CTX-008, AG-RET-005, AG-INC-005 | memory audit, invalidation, purge, source check. |
| KNO-08 Doc-to-graph pipeline | AG-CTX-007, AG-CTX-011, AG-RET-007 | source graph record, relations sourcées, contradiction report. |
| KNO-09 Knowledge narrative packaging | AG-QUA-002, AG-RET-001, AG-AUD-001 | package narratif sourcé, claim ledger, owner et validité. |
| KNO-10 Source Graph Resolver | AG-CTX-008, AG-CTX-011, AG-QUA-002 | source graph query, supersession check, contradiction decision. |
| RUN-01 Dynamic factory contrôlée | AG-DYN-001 à AG-DYN-005 | registre de capacité dynamique, expiration, validation. |
| RUN-02 Runtime output governance | AG-TOL-007, AG-RET-006 | registre surfaces runtime, rétention, statut d'indexation. |
| RUN-03 Kubernetes agent control plane | AG-TOL-001, AG-TOL-007, AG-OBS-004 | runtime provider contract, quotas, service account, OTel. |
| RUN-04 Orders exec/formula dispatcher | AG-TOL-001, AG-QUA-001 | order dispatcher contract, budget, preuve attendue. |
| RUN-05 Primitive-first capability model | AG-DYN-001, AG-DYN-005 | capability pack, registry, tests de compétence. |
| RUN-06 Capability marketplace | AG-DYN-004, AG-DYN-005, AG-PAT-003 | capability pack, owner, statut, usage telemetry. |
| RUN-07 Skill/capability lifecycle | AG-DYN-002, AG-DYN-004, AG-PAT-003 | skill record, lifecycle status, eval de promotion. |
| RUN-08 Runtime provider contract | AG-TOL-007, AG-OBS-003 | runtime provider contract, health, logs, cleanup. |
| RUN-09 Agent backend boundary | AG-LLM-001, AG-TOL-001, AG-OBS-003 | provider registry, adapter contract, fallback explicite. |
| RUN-10 Local agent worker pool | AG-ORC-004, AG-TOL-007, AG-OBS-004 | worker pool queue, WIP limit, health report. |
| RUN-11 Workspace isolation | AG-TOL-001, AG-TOL-004, AG-OBS-003 | workspace policy, path allowlist, secret scan, teardown. |
| RUN-12 Secure local coordinator | AG-TOL-004, AG-TOL-007, AG-OBS-003 | signed inbox, session log, env scrub, no token proxy evidence. |

## Lecture par preuve

| Preuve | Patterns principaux |
| --- | --- |
| Brief agentique | ORG-01 |
| Carte Kanban | ORG-01, ORC-01 |
| Task envelope | ORC-02, ORC-05, GOV-01 |
| Context pack | ORC-05, ORC-06, ORC-08 |
| Handoff packet | ORC-03, QUA-01, KNO-04 |
| Claim ledger | QUA-01, QUA-04 |
| Evidence pack | QUA-04, QUA-05 |
| Verification verdict | ORG-02, QUA-04, QUA-05 |
| Mission ledger | QUA-03, ORC-03 |
| Source registry | ORC-04, ORC-06, KNO-02 |
| Knowledge source index | KNO-06, ORC-04, ORC-05 |
| Workflow state manifest | ORC-09, QUA-05 |
| Flow DSL minimal | ORC-10, ORC-09 |
| Guardrail contract | GOV-08, GOV-01 |
| Browser tool contract | QUA-11, GOV-07 |
| Eval dataset record | QUA-09, MOD-01 |
| Source graph record | KNO-08, ORC-07 |
| Source graph query | KNO-10, ORC-07 |
| Memory routing policy | KNO-07, ORC-06 |
| Runtime provider contract | RUN-08, RUN-03, RUN-10 |
| Capability pack | RUN-06, RUN-05 |
| Skill record | RUN-07 |
| Retention registry | KNO-01, KNO-04, RUN-02 |
| Incident record | GOV-02, KNO-05 |

## Règle finale

Un pattern revendiqué doit pouvoir pointer vers au moins une exigence et une preuve. S'il ne produit aucune preuve, il reste une recommandation d'architecture, pas une capacité conforme.
