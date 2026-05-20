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
| GOV-01 Policy engine et hooks | AG-TOL-001, AG-TOL-002, AG-TOL-006 | policy manifest, hook registry, décisions allow/block/escalate. |
| GOV-02 Dry-run avant action risquée | AG-TOL-002, AG-INC-001, AG-QUA-007 | dry-run report, rollback plan, go/no-go. |
| GOV-03 Hook lifecycle progressif | AG-TOL-006, AG-INC-003 | mode shadow/canary/enforced, faux positifs, validation. |
| GOV-04 Autonomie gouvernée | AG-QUA-004, AG-TOL-002, AG-INC-001 | niveau d'autonomie, validation authority, blocages. |
| MOD-01 Model router | AG-LLM-001, AG-LLM-002, AG-LLM-005 | politique de routage, fallback, journal modèle. |
| MOD-02 Model retirement guard | AG-LLM-006 | statut modèle, fallback cible, eval de remplacement. |
| QUA-01 Claim ledger | AG-QUA-002 | claim ledger, source ou hypothèse liée. |
| QUA-02 Observabilité agentique | AG-LLM-004, AG-INC-004 | traces, métriques, SLO, coûts, latence. |
| QUA-03 Mission ledger append-only | AG-ORC-006 | mission ledger, événements append-only. |
| QUA-04 Evidence pack et verdict | AG-QUA-001, AG-QUA-006, AG-QUA-007 | evidence pack, verification verdict. |
| QUA-05 Evidence-driven transition | AG-ORC-006, AG-QUA-001, AG-QUA-007 | gate de transition, DoD, verdict lié. |
| KNO-01 Knowledge janitor | AG-RET-001, AG-RET-004 | cleanup report, registre de rétention. |
| KNO-02 Mémoire hybride | AG-CTX-007, AG-CTX-008 | memory audit, graphe, sidecar, source registry. |
| KNO-03 Doc drift detector | AG-RET-007 | rapport de drift, comparaison runtime/docs. |
| KNO-04 Knowledge promotion | AG-CTX-006, AG-RET-001, AG-RET-002 | mémoire candidate, preuve source, décision de promotion. |
| KNO-05 Memory contamination response | AG-INC-002, AG-RET-005 | incident, purge, correction, eval de prévention. |
| RUN-01 Dynamic factory contrôlée | AG-DYN-001 à AG-DYN-005 | registre de capacité dynamique, expiration, validation. |
| RUN-02 Runtime output governance | AG-TOL-007, AG-RET-006 | registre surfaces runtime, rétention, statut d'indexation. |

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
| Retention registry | KNO-01, KNO-04, RUN-02 |
| Incident record | GOV-02, KNO-05 |

## Règle finale

Un pattern revendiqué doit pouvoir pointer vers au moins une exigence et une preuve. S'il ne produit aucune preuve, il reste une recommandation d'architecture, pas une capacité conforme.
