# Matrice risques, contrôles et preuves

Cette matrice relie les risques agentiques aux contrôles et preuves nécessaires. Elle complète les matrices exigences -> preuves et patterns -> exigences -> preuves.

## Matrice principale

| Risque | Contrôles | Preuves | Télémétrie |
| --- | --- | --- | --- |
| Mission floue | CTRL-MIS-001, CTRL-AUT-001 | brief, questions, DoR | taux missions bloquées pour ambiguïté. |
| Hallucination | CTRL-CTX-002, CTRL-QUA-001 | claim ledger, source active | claims sans preuve, corrections. |
| RAG aveugle | CTRL-CTX-001, CTRL-CTX-003 | context pack, sources exclues | sources superseded rejetées. |
| Base de connaissance hors scope | CTRL-CTX-001, CTRL-SEC-001, CTRL-RET-002 | knowledge source index, ACL, freshness report | sources rejetées, résultats filtrés, réindexations. |
| Corpus externe obsolète | CTRL-CTX-003, CTRL-RET-002 | freshness report, source registry, désindexation | sources stale, réindexations, quarantines. |
| Contexte trop large | CTRL-CTX-004 | justification budget, résumé sourcé | tokens, budget, escalades deep. |
| Contexte insuffisant | CTRL-CTX-002 | scorecard warning/failed | relances contexte, questions client. |
| Source contradictoire | CTRL-CTX-003 | décision de conflit, escalade | conflits par mission. |
| Modèle non autorisé | CTRL-MOD-001, CTRL-MOD-002 | policy route, fallback | rejets modèle, fallback rate. |
| Provider LLM non déclaré | CTRL-MOD-001, CTRL-OBS-001 | llm-provider-registry, blocage pre-model-route | appels bloqués hors registry, fallback provider. |
| Fallback provider dangereux | CTRL-MOD-002, CTRL-SEC-001 | fallback chain validée, policy data | divergences provider, blocages données sensibles. |
| Donnée sensible exposée | CTRL-SEC-001, CTRL-OBS-002 | blocage, masquage, incident | secrets bloqués, exports rejetés. |
| Prompt injection | CTRL-SEC-002 | rapport blocage, source isolée | injections détectées. |
| Source distante obsolète | CTRL-CTX-003, CTRL-RET-002 | remote audit, ref freshness, source quarantine | refs rejetées, remotes inaccessibles, dirty skip. |
| Outil mal utilisé | CTRL-TOL-001, CTRL-TOL-002 | policy decision, blast radius | actions bloquées, erreurs outil. |
| Blast-radius outil trop large | CTRL-TOL-001, CTRL-TOL-002, CTRL-OBS-001 | tool scope, allowlist, dry-run, policy decision | scopes rejetés, escalades, dépassements budget. |
| Serveur MCP non fiable | CTRL-TOL-001, CTRL-SEC-001, CTRL-OBS-001 | contrat MCP, scopes, env vars, trust gate | MCP bloqués, tools refusés, timeouts. |
| Action irréversible | CTRL-DRY-001 | dry-run, rollback, go/no-go | dry-runs requis/passés. |
| Action cluster dangereuse | CTRL-DRY-001, CTRL-TOL-002, CTRL-SEC-001 | dry-run cluster, impact report, rollback plan | applies bloqués, diff critiques, rollback tests. |
| Politique d'environnement confondue | CTRL-TOL-001, CTRL-AUT-001 | environment policy, validation authority, audit prod | actions prod bloquées, overrides, exceptions. |
| Faux Done | CTRL-QUA-002, CTRL-QUA-003 | evidence pack, verdict | fermetures sans preuve, reopen rate. |
| Transition workflow non prouvée | CTRL-QUA-002, CTRL-QUA-003 | workflow state manifest, transition event, evidence pack | transitions bloquées, preuves manquantes. |
| Validation circulaire | CTRL-AUT-001, CTRL-QUA-003 | validateur distinct | validations par domaine. |
| Décision critique mono-modèle | CTRL-AUT-001, CTRL-QUA-003, CTRL-MOD-001 | council record, quorum, dissent log, veto | décisions council, désaccords, escalades. |
| Mémoire contaminée | CTRL-RET-001, CTRL-INC-001 | incident, purge, memory audit | invalidations mémoire. |
| Mémoire utilisée hors autorité | CTRL-CTX-003, CTRL-RET-001 | memory routing policy, source active, audit mémoire | mémoires rétrogradées, conflits détectés. |
| Drift documentaire | CTRL-RET-002, CTRL-PAT-001 | rapport drift, correction | drifts ouverts/fermés. |
| Graphe documentaire non sourcé | CTRL-CTX-003, CTRL-QUA-001 | source graph record, claim ledger, relation provenance | relations rejetées, contradictions. |
| Coût anormal | CTRL-CTX-004, CTRL-SLO-001 | budget escalation, alerte SLO | coût par carte, tokens, latence. |
| Observabilité insuffisante | CTRL-OBS-001 | trace completeness report | spans manquants, logs non corrélés. |
| Version prompt non attribuable | CTRL-OBS-001, CTRL-SLO-001 | prompt version, eval dataset, canary/rollback | régressions par version, rollbacks. |
| Trajectoire agent non rejouable | CTRL-OBS-001, CTRL-QUA-002 | trajectory log, mission ledger, evidence links | événements manquants, gaps de causalité. |
| Browser automation risquée | CTRL-TOL-001, CTRL-DRY-001, CTRL-QUA-002 | browser tool contract, DOM snapshot, screenshot, network logs | actions UI bloquées, preuves visuelles manquantes. |
| Preuve visuelle insuffisante | CTRL-QUA-002, CTRL-OBS-001 | visual evidence pack, DOM snapshot, screenshot | packs incomplets, captures manquantes. |
| Workspace non isolé | CTRL-TOL-001, CTRL-SEC-001 | workspace policy, path allowlist, secret scan, teardown | accès hors scope, secrets bloqués. |
| Runtime provider opaque | CTRL-OBS-001, CTRL-TOL-001 | runtime provider contract, health, logs, cleanup | unhealthy sessions, cleanups échoués. |
| Capability proliférante | CTRL-PAT-001, CTRL-RET-002 | capability pack, skill record, lifecycle status | capacités retirées, usages faibles, expirations. |
| Coordination locale dangereuse | CTRL-TOL-001, CTRL-SEC-001, CTRL-OBS-001 | signed inbox, env scrub, no token proxy, session log | proxys refusés, sessions isolées. |

## Sévérité

| Sévérité | Critère | Réponse minimale |
| --- | --- | --- |
| low | impact local, réversible. | trace et correction normale. |
| medium | rework ou coût significatif. | carte correction, owner, preuve. |
| high | sécurité, client, production ou décision durable. | validation, incident possible, réduction autonomie. |
| critical | fuite, suppression, action irréversible ou faux Done critique. | containment immédiat, incident, post-mortem. |

## Règle finale

Un risque sans contrôle est une dette. Un contrôle sans preuve est invisible. Une preuve sans télémétrie est difficile à améliorer.
