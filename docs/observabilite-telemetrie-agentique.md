# Observabilité et télémétrie agentiques

Cette page détaille la collecte des traces, métriques, logs et événements nécessaires pour gouverner une entreprise-agent. Elle complète [observabilite-evals-slo-agentiques.md](observabilite-evals-slo-agentiques.md) en formalisant la télémétrie.

## Principes

| Principe | Règle |
| --- | --- |
| Corrélation | Tous les signaux importants partagent mission_id, task_id et trace_id. |
| Minimisation | Ne pas exporter secrets, prompts sensibles ou données personnelles inutiles. |
| Explicabilité | Chaque décision durable doit être reliée à contexte, contrôle, preuve et verdict. |
| Proportionnalité | Plus le risque est élevé, plus la télémétrie doit être complète. |
| Rétention | Les traces temporaires ont TTL ; les verdicts et incidents critiques peuvent durer plus longtemps. |

## Modèle de signaux

| Signal | Usage | Exemple |
| --- | --- | --- |
| Trace | Reconstituer un run bout en bout. | mission -> contexte -> modèle -> outil -> verdict. |
| Span | Mesurer une étape. | récupération contexte, appel modèle, hook pre-tool. |
| Log | Capturer diagnostic ou erreur. | outil en erreur, fallback modèle. |
| Metric | Mesurer tendance ou SLO. | coût par carte, faux Done évités. |
| Event | Marquer décision ponctuelle. | autonomie downgradée, source quarantined. |
| Baggage | Propager contexte non sensible. | mission_id, risk_level, autonomy_level. |

## Spans minimaux

| Span | Attributs minimaux |
| --- | --- |
| agent.mission | mission_id, risk_level, client_scope, validator. |
| agent.workflow.transition | workflow_id, from_state, to_state, guard, evidence_pack_id, decision. |
| agent.workflow.interrupt | workflow_id, state, interrupt_type, authority, resume_state. |
| agent.context.load | context_profile, budget, source_count, rejected_source_count. |
| agent.context.score | sufficiency, freshness, coherence, sensitivity, confidence. |
| agent.model.route | provider, model, fallback_provider, fallback_model, risk_level, policy_decision. |
| agent.model.call | provider, model, prompt_version, input_tokens, output_tokens, latency_ms, error. |
| agent.tool.call | tool_name, tool_risk, blast_radius, policy_decision, duration_ms, error. |
| agent.hook.evaluate | hook_id, mode, decision, reason. |
| agent.subagent.run | role, task_id, autonomy_level, handoff_status. |
| agent.evidence.pack | evidence_pack_id, criteria_covered, missing_evidence. |
| agent.verdict | verdict_id, result, decision, validator. |
| agent.trajectory.event | step, actor_id, action, observation_ref, decision_ref. |
| agent.browser.evidence | url_scope, action_type, dom_snapshot_id, screenshot_id, network_log_id. |
| agent.capability.resolve | capability_id, skill_id, version, lifecycle_status, tests_status. |
| agent.runtime.session | provider_id, workspace_id, health, duration_ms, cleanup_status. |
| agent.memory.write | memory_id, retention_class, indexable, sensitivity. |
| agent.pricing.resolve | pricing_source, model, provider, precedence_layer, unit_price_version. |
| agent.reliability.aggregate | model, prompt_version, rig, sessions, crashed, quarantined, idle_killed. |
| agent.incident | incident_id, severity, containment, status. |

## Métriques recommandées

| Métrique | Type | Usage |
| --- | --- | --- |
| agent_tasks_total | counter | volume de tâches. |
| agent_task_duration_seconds | histogram | latence par rôle et étape. |
| agent_context_budget_total | counter | répartition tiny/small/medium/deep. |
| agent_context_escalations_total | counter | escalades de budget. |
| agent_model_tokens_total | counter | tokens par modèle, rôle et mission. |
| agent_model_cost_estimated_total | counter | coût estimé par modèle, provider, rig et mission. |
| agent_model_fallback_total | counter | robustesse et retrait modèle. |
| agent_prompt_version_regressions_total | counter | régressions par prompt, skill, modèle ou provider. |
| agent_tool_blocks_total | counter | actions bloquées. |
| agent_tool_blast_radius_reductions_total | counter | appels outils réduits ou basculés en dry-run. |
| agent_runtime_sessions_total | counter | sessions par runtime provider et health final. |
| agent_false_done_prevented_total | counter | faux Done évités. |
| agent_evidence_coverage_ratio | gauge | couverture des critères. |
| agent_slo_breaches_total | counter | violations de SLO. |
| agent_session_crash_rate_ratio | gauge | CrashRate par modèle, prompt version et rig. |
| agent_session_unhealthy_rate_ratio | gauge | UnhealthyRate par modèle, prompt version et rig. |
| agent_session_quarantined_total | counter | sessions mises en quarantaine. |
| agent_session_idle_killed_total | counter | sessions arrêtées par inactivité. |
| agent_memory_invalidations_total | counter | mémoire contaminée ou obsolète. |
| agent_exceptions_open_total | gauge | dette de conformité. |

## Événements normatifs

| Event | Quand |
| --- | --- |
| autonomy.downgraded | risque, incident ou preuve manquante réduit l'autonomie. |
| context.conflict_detected | sources critiques contradictoires. |
| context.budget_escalated | budget augmenté. |
| source.quarantined | source suspecte ou sensible isolée. |
| model.disallowed_blocked | modèle interdit bloqué. |
| model.provider_disallowed_blocked | provider non déclaré ou interdit bloqué. |
| prompt.version_regressed | prompt, skill ou instructions en régression sur eval. |
| model.cost_budget_exceeded | coût estimé ou réel dépasse le budget autorisé. |
| tool.blast_radius_limited | outil limité par périmètre. |
| workflow.transition_blocked | transition refusée faute de guard ou preuve. |
| browser.action_blocked | action navigateur hors scope ou risquée. |
| capability.lifecycle_changed | capability pack ou skill promu, déprécié ou retiré. |
| runtime.session_unhealthy | crash, quarantine, idle kill ou drain anormal détecté. |
| runtime.failure_classified | échec classifié transient ou hard avant retry/escalade. |
| runtime.controller_token_scrubbed | token d'infrastructure retiré avant spawn d'une session agent. |
| evidence.missing | fermeture refusée faute de preuve. |
| compliance.exception_opened | exception de conformité créée. |
| memory.contamination_detected | mémoire polluée détectée. |
| pattern.lifecycle_changed | pattern promu, déprécié ou retiré. |

## Politique de logs

| Contenu | Règle |
| --- | --- |
| Prompt complet | éviter par défaut ; stocker digest ou extrait minimisé si nécessaire. |
| Réponse modèle | stocker résumé ou digest si sensible. |
| Paramètres outil | masquer secrets, tokens, chemins sensibles si requis. |
| Données client | minimiser, classifier, appliquer rétention. |
| Erreurs | conserver message utile, stack si non sensible, corrélation trace_id. |

## Sampling

| Situation | Sampling recommandé |
| --- | --- |
| Tâche faible risque réussie | échantillonnage partiel possible. |
| Tâche à risque | trace complète. |
| Action bloquée | trace complète. |
| Incident | trace complète + rétention renforcée. |
| Données sensibles | trace minimisée, attributs masqués, stockage autorisé seulement. |

## Dashboards minimaux

| Dashboard | Questions |
| --- | --- |
| Santé agentique | runs, erreurs, blocages, latence, coût. |
| Contexte | budgets, conflits, sources rejetées, cache hit. |
| Modèles | coûts, fallback, erreurs, modèles bloqués. |
| Outils | appels, blocages, blast radius, incidents. |
| Qualité | evidence coverage, verdicts, rework, faux Done. |
| Conformité | exceptions, exigences non couvertes, audits, SLO breaches. |
| Mémoire | promotions, invalidations, purges, sources superseded. |

## Règle finale

La télémétrie doit expliquer sans exposer. Elle doit donner assez de signaux pour auditer et améliorer, sans devenir une fuite de contexte ou une mémoire parallèle incontrôlée.
