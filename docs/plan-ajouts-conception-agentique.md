# Plan complet d'ajouts à la conception agentique

Ce plan fusionne les enseignements des 37 projets analysés dans `/mnt/Travail/Projets/Dev/Référence-Agentique/`. Il ne cherche pas à copier des frameworks : il transforme les features récurrentes en ajouts normatifs, design patterns, contrats, contrôles et options de runtime pour notre conception agentique.

## Principes de merge

| Principe | Règle |
| --- | --- |
| Extraire l'invariant | Un pattern est retenu seulement si plusieurs projets montrent le même besoin ou si un projet apporte une brique très nette. |
| Ne pas dépendre d'un outil | LangGraph, Dify, OpenHands, kagent, Langfuse ou gascity inspirent le design, mais ne deviennent pas des dépendances normatives. |
| Séparer pattern, contrôle et feature | Un pattern décrit la structure, un contrôle bloque/autorise, une feature est une capacité opérationnelle activable. |
| Garder les profils de maturité | Tout n'est pas requis au niveau minimal ; les briques lourdes vont dans les profils gouverné, mature ou production. |
| Tout relier aux preuves | Chaque ajout doit produire un contrat, une trace, un modèle ou une preuve vérifiable. |

## Résumé stratégique

| Axe | Décision de conception |
| --- | --- |
| Orchestration | Passer d'un orchestrateur conversationnel à un `Workflow State Engine` durable, interruptible et observable. |
| Contexte | Faire de l'`Advanced Context Orchestrator` un plan d'infrastructure : sources, graphe, RAG, mémoire, compression, conflits et budgets. |
| Base de connaissance | Ajouter une couche `Knowledge Base Indexer` distincte de la mémoire et du contexte : elle greffe des corpus externes gouvernés (repo, URL, API, MCP, base de données, dossier) et les rend recherchables. |
| Runtime | Définir trois profils : local worker pool, workflow durable, Kubernetes agent control plane. |
| Capacités | Traiter skills, packs, MCP, hooks et agents comme des capacités versionnées avec lifecycle. |
| Sécurité | Combiner sandbox, blast-radius, prompt injection firewall, remote hygiene, MCP trust et séparation controller/agent. |
| Observabilité | Rendre obligatoires traces, tool calls, coûts, evals, evidence, trajectoires et SLO dès le profil gouverné. |
| Preuves | Remplacer le Done déclaratif par des transitions evidence-gated, claim ledger, visual evidence et verification verdict. |
| UX/UI | Ajouter une famille de preuves visuelles : DOM, capture, parcours, UI state trace et design authority. |
| Documentation | Maintenir la doc comme un référentiel vivant : pattern record, maturité, drift, promotion, purge et anti-patterns. |

## Matrice projet -> ajouts à récupérer

| Projet | Ajouts/features à récupérer | Destination principale |
| --- | --- | --- |
| agent-framework | Profil multi-runtime, agents déclaratifs, contrats d'agents, compatibilité Python/.NET sans dépendance fournisseur. | Runtime provider, agent backend boundary, capability profile. |
| agent-sandbox | Isolation d'outils, sandbox policy, preuves d'exécution isolée, environnements Kubernetes/dev. | Tool blast-radius, workspace isolation, K8s control plane. |
| agent-skills | Packaging de skills, lifecycle skill, promotion/purge de capacité. | Capability marketplace, skill record, capability lifecycle. |
| ai-agents-for-beginners | Taxonomie pédagogique, parcours de maturité, trustworthy agents, cartes d'apprentissage. | Pattern maturity map, learning cards, documentation progressive. |
| andrej-karpathy-skills | Format skill minimal, activation par dossier, anti-prolifération. | Skill record minimal, progressive disclosure, anti-pattern skills. |
| autogen | Équipes multi-agents, conversation contrôlée, human-in-the-loop, handoff vérifiable. | Team/crew pattern, conversation control, handoff primitive. |
| BMAD-METHOD | Rôles spécialisés, RACI agentique, DoR/DoD, workflow guidé. | Organisation, pilotage, evidence-gated workflow. |
| browser-use | Contrat browser tool, vision/DOM, preuves visuelles, blast-radius web. | Browser tool contract, visual evidence pack, UI validation. |
| claude-octopus | Swarm contrôlé, coordination parallèle, council/review. | Decision council gate, local worker pool, parallel coordination. |
| claude-skills | Skill registry normatif, fiche skill, tests de compétence, activation par compétence. | Capability marketplace, skill record, competency tests. |
| CodeGraphContext | Context pack enrichi par graphe, source graph comme preuve contextuelle. | Source graph resolver, context constitution, source graph record. |
| conductor | State machine, persistence, schedulers, retry/timeout/compensation. | Workflow State Engine, workflow-state-manifest. |
| crewAI | Crew par rôle, role contract, process mode séquentiel/hiérarchique. | Role contract, crew pattern, process mode. |
| Design | Preuves UX, validation design authority, diagrammes UI agentique. | Visual evidence pack, design validation authority. |
| dify | Visual workflow builder, datasets/RAG, plugins/outils, ops app agentique. | Visual workflow manifest, RAG component contract, agent backend boundary. |
| everything-claude-code | Hooks, prompt registry, runtime surface governance, install profiles. | Hook lifecycle, runtime surface registry, prompt lifecycle. |
| gas town | Beads, packs, marketplace, OTEL, terminal/tmux adapter, K8s provider, pricing, reliability. | Capability marketplace, telemetry plane, runtime provider, cost/reliability SLO. |
| graphify | Doc-to-graph, memory graph pipeline, contradiction detection. | Source graph resolver, doc-to-graph, contradiction detection. |
| haystack | Pipeline retrieval, RAG components, document stores, eval RAG. | RAG component contract, eval dataset lifecycle. |
| kagent | Ops agent authority, cluster action dry-run, policy by environment, Kubernetes agents. | K8s control plane, cluster dry-run, policy by environment. |
| langflow | Diagrammes exécutables, visual flow registry, components UI. | Visual workflow manifest, workflow visual registry. |
| langfuse | Traces LLM, prompt/version observability, eval datasets, metrics. | Agent telemetry plane, prompt registry, eval lifecycle. |
| langgraph | StateGraph, checkpoint/resume, interrupts, durable execution. | Workflow State Engine, human interrupt contract. |
| LLMLingua | Prompt compression, budget contextuel, réduction token. | Context compression gate, context budget escalation/descente. |
| LLMSecurityGuide | Threat model, prompt injection, data leakage, controls. | Security control catalog, prompt injection firewall. |
| mempalace | Memory palace, memory routing, recall confidence. | Memory routing policy, memory integrity, hybrid memory. |
| Octogent | Worker pool/DAG, source inaccessible, source quarantine. | Local worker pool, source quarantine, remote hygiene. |
| openai-agents-python | Guardrails, handoffs, tracing, tools as primitives. | Guardrail contract, handoff primitive, tracing baseline. |
| openclaw | Remote hygiene, release telemetry, branch/ref audit, gateway multi-canal. | Remote Hygiene Guard, release telemetry, multi-channel dispatch. |
| OpenHands | Coding-agent runtime, workspace sandbox, browser/terminal, trajectory logging. | Coding-agent runtime model, workspace isolation, trajectory logging. |
| OpenMythos | Knowledge narrative packaging, domain storylines. | Domaine/mémoire pédagogique optionnelle, jamais source de vérité. |
| pixel-agents | Visual state, UI automation, pixel/vision proof. | UI state trace, visual evidence pack. |
| ruflo | Workflow DSL minimal, flow validation, routing modèle/mémoire/ADR. | Flow DSL minimal, router policy, ADR routing. |
| shannon | Research trace, deep reasoning budget, pipeline Temporal sécurité. | Research trace, reasoning budget, evidence-gated pipeline. |
| superpowers | Permissioned superpowers, hard gates, capability marketplace. | Capability marketplace, permissioned capability, hard-gated skills. |
| switchboard | Router policy, multi-channel dispatch, inbox HMAC, evidence workflow. | Secure local coordinator, router policy, multi-channel dispatch. |
| vscode-copilot-chat | IDE context governance, tool UX, telemetry privacy, grouped tools. | IDE context governance, tool relevance grouper, telemetry privacy model. |

## Backlog de merge par famille

### 1. Organisation, rôles et pilotage

| Ajout | Type | Sources | Intégration |
| --- | --- | --- | --- |
| RACI agentique | Ajuster design existant | BMAD-METHOD, crewAI, AutoGen | Étendre `architecture-pilotage-agentique.md` et `modele-reference-structure-agentique.md` avec responsabilités par rôle. |
| Role contract / crew pattern | Nouveau pattern | crewAI, AutoGen, OpenAI Agents SDK, agent-framework | Ajouter un pattern organisation/runtime : rôle, outils, limites, handoff, validation. |
| Conversation contrôlée | Nouveau contrôle | AutoGen, OpenAI Agents SDK | Définir règles de dialogue multi-agent : tour, arrêt, human interrupt, preuve de conclusion. |
| Parcours de maturité pédagogique | Documentation | ai-agents-for-beginners, BMAD-METHOD | Ajouter une carte de lecture par niveau : minimal, contrôlé, orchestré, gouverné, mature. |
| Decision council renforcé | Ajuster pattern | Claude Octopus, AutoGen, OpenAI Agents SDK | Préciser quorum, veto, budget, trace de désaccord et limite de coût. |

### 2. Orchestration, graphes et workflows

| Ajout | Type | Sources | Intégration |
| --- | --- | --- | --- |
| Workflow State Engine | Nouveau pattern central | LangGraph, Conductor, Dify, Langflow, Shannon | Définir graphes durables, checkpoints, resume, retries, compensations, interrupts. |
| State machine normative | Contrat | Conductor, LangGraph, Switchboard | Créer `workflow-state-manifest.md` : états, transitions, guards, retries, preuves. |
| Human interrupt contract | Contrat | LangGraph, AutoGen, OpenAI Agents SDK | Ajouter un modèle d'interruption : raison, contexte, choix permis, reprise. |
| Visual workflow manifest | Feature/design | Dify, Langflow | Accepter builders visuels si export manifest auditable + diagramme Mermaid. |
| Flow DSL minimal | Feature à surveiller/intégrer | ruflo, Shannon | Définir un DSL minimal optionnel pour workflows simples sans moteur lourd. |
| Handoff as primitive | Ajuster contrat | OpenAI Agents SDK, AutoGen, crewAI | Renforcer `handoff-packet.md` : propriétaire, preuves, hypothèses, risques, prochaine action. |

### 3. Base de connaissance, contexte, mémoire et connaissances

| Ajout | Type | Sources | Intégration |
| --- | --- | --- | --- |
| Knowledge Base Indexer | Nouveau pattern | Haystack, Dify, Langflow, CodeGraphContext, graphify, VS Code Copilot Chat | Ajouter une base de connaissance indexée, distincte de la mémoire agentique : connecteurs repo/URL/API/MCP/DB/dossier, indexation, recherche, ACL, fraîcheur, provenance. |
| Source Graph Resolver | Nouveau pattern | CodeGraphContext, graphify, Haystack | Relier code, docs, décisions, preuves et contradictions dans un graphe consultable. |
| Context constitution | Ajuster design | VS Code Copilot Chat, LLMLingua, Haystack | Définir constitution du contexte : sources actives > graph/RAG > mémoire > similarité. |
| Context Compression Gate | Contrôle | LLMLingua, VS Code Copilot Chat | Autoriser compression seulement si provenance, contraintes et tool-call atomicity restent intactes. |
| RAG component contract | Contrat | Haystack, Dify, Langflow | Définir retriever, ranker, document store, eval, freshness et contamination policy. |
| Memory palace / memory routing | Pattern mémoire | mempalace, graphify | Ajouter routage mémoire L0-L3, confiance de rappel et règles de promotion. |
| Contradiction detection | Feature | graphify, CodeGraphContext | Ajouter détection contradictions entre sources et mémoire avant synthèse. |
| Source quarantine | Contrôle | Octogent, openclaw | Mettre en quarantaine remote inaccessible, source obsolète ou contenu suspect. |
| Knowledge narrative packaging | Feature optionnelle | OpenMythos | Utiliser des storylines de domaine seulement comme couche pédagogique, jamais source de vérité. |

### 4. Runtime, agents et surfaces d'exécution

| Ajout | Type | Sources | Intégration |
| --- | --- | --- | --- |
| Agent Backend Boundary | Nouveau pattern | Dify, OpenHands, agent-framework | Séparer node workflow, backend agent, transport d'événements, SDK et outils. |
| Coding-agent runtime model | Pattern runtime | OpenHands, VS Code Copilot Chat, openclaw | Définir workspace, terminal, navigateur, fichiers, events, sandbox et trajectoire. |
| Local Agent Worker Pool | Pattern runtime | Octogent, Conductor, gas town, Claude Octopus | Slots, queue, cancellation, retries, health, coût et evidence par worker. |
| Kubernetes Agent Control Plane | Profil production | kagent, agent-sandbox, gascity | CRDs/policies/provider natif, quotas, service accounts, network allowlists, OTel. |
| Runtime provider contract | Contrat | gascity, agent-sandbox, OpenHands | Uniformiser tmux/subprocess/exec/ACP/K8s : lifecycle, exec, logs, ressources, health. |
| Workspace isolation | Contrôle/runtime | OpenHands, agent-sandbox | Définir workspace root, fichiers autorisés, réseau, secrets, teardown et preuves. |
| Orders exec/formula dispatcher | Feature runtime | gascity | Distinguer shell-only sans session agent vs workflow agentique avec budget/proof. |
| Browser tool contract | Contrat outil | browser-use, pixel-agents, OpenHands | DOM, capture, action, scope URL, permissions, preuve visuelle, rollback impossible. |
| IDE context governance | Feature runtime | VS Code Copilot Chat | Gouverner contexte IDE, sélection de fichiers, tools, prompts et privacy telemetry. |

### 5. Capacités, skills, packs et marketplace

| Ajout | Type | Sources | Intégration |
| --- | --- | --- | --- |
| Capability Marketplace | Nouveau pattern | agent-skills, claude-skills, superpowers, gas town | Registry de capacités : owner, permissions, tests, version, statut, expiration. |
| Skill record normatif | Modèle | claude-skills, agent-skills, Andrej Karpathy skills | Ajouter `skill-record.md` ou étendre `fiche-subagent.md` pour activation, outils, limites. |
| Capability pack manifest | Contrat | gascity-packs, agent-framework | Définir imports, prompts, rôles, permissions, tests, compatibilité runtime. |
| Progressive disclosure | Design | claude-skills, superpowers | Charger seulement la compétence utile ; lazy-load de docs et références. |
| Tests de compétence | Contrôle | claude-skills, superpowers | Un pack promu doit avoir exemples, tests, preuve d'usage et critères d'échec. |
| Anti-prolifération skills | Contrôle | Andrej Karpathy skills, agent-skills | Durée de vie, purge, fusion, propriétaire et score de réutilisation. |
| Permissioned superpower | Feature | superpowers | Toute capacité puissante doit déclarer scope, risques, dry-run et preuve. |
| Primitive-first capability model | Design | gascity, agent-framework | Les rôles sont configs/packs, pas types SDK hardcodés. |

### 6. Outils, MCP et intégrations

| Ajout | Type | Sources | Intégration |
| --- | --- | --- | --- |
| Tool registry enrichi | Ajuster existant | OpenAI Agents SDK, OpenHands, VS Code Copilot Chat | Ajouter owner, risque, inputs, outputs, side effects, preuve, budget, permissions. |
| MCP Trust Gate | Contrôle | VS Code Copilot Chat, beads-mcp, agent-framework | Vérifier origine, permissions, env vars, capabilities, logging et blast-radius. |
| Tool Blast-Radius Limiter | Contrôle central | agent-sandbox, browser-use, OpenHands, kagent | Limiter fichiers, réseau, production, coût, shell, navigateur et cloud. |
| Multi-channel dispatch | Feature | switchboard, openclaw | Router demandes via inbox/terminal/webhook/chat avec signature et policy. |
| Router policy | Contrôle | switchboard, ruflo | Formaliser règles de routage : canal, priorité, propriétaire, modèle, outil, preuve. |
| Remote Hygiene Guard | Contrôle | openclaw, Octogent | Branch/ref audit, remote inaccessible, tags massifs, source freshness, quarantine. |

### 7. Sécurité, gouvernance et conformité

| Ajout | Type | Sources | Intégration |
| --- | --- | --- | --- |
| Threat model agentique | Documentation/contrôle | LLMSecurityGuide, OWASP LLM | Couvrir injection, data leakage, tool abuse, prompt exfiltration, memory poisoning. |
| Prompt Injection Firewall | Contrôle | LLMSecurityGuide, browser-use | Isoler contenu externe et instructions système ; refuser ordre venant d'une page/source. |
| Guardrail contract | Contrat | OpenAI Agents SDK, kagent, agent-sandbox | Définir input/output guardrails, décisions, preuve, fallback et incident. |
| Cluster action dry-run | Contrôle | kagent, agent-sandbox | Toute action cluster/infra passe par plan, impact, policy, validation et rollback. |
| Agent Privilege Boundary | Contrôle | gascity, OpenHands, Switchboard | Séparer permissions controller/agent, scrub tokens, protéger clés d'infrastructure. |
| Autonomy Level Gate | Ajuster existant | OpenHands, browser-use, BMAD | Niveau d'autonomie par risque, réversibilité, preuve, coût et autorité. |
| Policy by environment | Contrôle | kagent, OpenHands | Règles différentes local/staging/prod, données sensibles, réseau, secrets. |
| Security control catalog | Documentation | LLMSecurityGuide | Catalogue de contrôles mappé à risques, preuves et niveaux de conformité. |

### 8. Observabilité, evals et SLO

| Ajout | Type | Sources | Intégration |
| --- | --- | --- | --- |
| Agent Telemetry Plane | Pattern central | Langfuse, OpenAI Agents SDK, gascity-otel, Octogent | Traces, spans, tool calls, coûts, evals, evidence, incidents, SLO. |
| Prompt/version observability | Feature | Langfuse, VS Code Copilot Chat | Versionner prompts, datasets, résultats, regressions et rollbacks. |
| Eval dataset lifecycle | Contrat | Langfuse, Haystack, OpenAI Agents SDK | Dataset, expected output, judge, seuil, drift, promotion. |
| Trajectory logging | Feature | OpenHands, Octogent | Journaliser trajectoire agent : état, action, résultat, observation, décision. |
| LLM Cost Registry | Feature/contrat | gascity, Langfuse | Coût par modèle/provider/rig, budget, fallback, dépassement. |
| Session Reliability SLO Reporter | Feature/SLO | gascity, OpenHands | CrashRate, UnhealthyRate, idle kills, quarantines, drains par model/rig. |
| Release telemetry | Feature | openclaw, Langfuse | Relier release, branch/ref freshness, evals et incidents après merge. |
| Telemetry privacy model | Contrôle | VS Code Copilot Chat, Langfuse | Masquage, minimisation, rétention, digest, opt-in prompt/tool content. |

### 9. Preuves, QA et validation visuelle

| Ajout | Type | Sources | Intégration |
| --- | --- | --- | --- |
| Evidence-Gated Workflow FSM | Pattern qualité | Switchboard, BMAD, Shannon, superpowers | Une transition ne passe que si preuves attendues et verdict existent. |
| Visual Evidence Pack | Pattern preuve | browser-use, pixel-agents, Design | DOM, screenshot, parcours, état visuel, critères UX, limite navigateur. |
| UI State Trace | Feature | pixel-agents, browser-use | Tracer état UI avant/après action, source visuelle et selectors. |
| Design Validation Authority | Rôle/contrôle | Design, pixel-agents | Autorité dédiée aux écarts design/UX, accessibilité et rendu. |
| Claim ledger renforcé | Ajuster existant | Switchboard, OpenHands, Langfuse | Chaque claim critique pointe vers source, outil, trace, capture ou hypothèse. |
| Verification verdict enrichi | Ajuster existant | OpenAI Agents SDK, BMAD | Ajouter décision, couverture, risques résiduels, retry/escalade. |

### 10. Documentation, lifecycle et amélioration continue

| Ajout | Type | Sources | Intégration |
| --- | --- | --- | --- |
| Pattern maturity map | Documentation | ai-agents-for-beginners, BMAD | Relier patterns aux niveaux minimal/contrôlé/orchestré/gouverné/mature. |
| Pattern learning cards | Documentation | ai-agents-for-beginners | Résumer chaque pattern : problème, usage, anti-pattern, preuve. |
| Doc-to-graph pipeline | Feature | graphify, CodeGraphContext | Convertir docs/patterns en graphe pour relations, contradictions et couverture. |
| Doc drift detector | Ajuster existant | graphify, runtime output governance | Détecter divergence entre runtime, docs, diagrams, templates et matrices. |
| Runtime surface cleanup | Ajuster existant | everything-claude-code, OpenHands | TTL, purge, archive, désindexation, promotion des artefacts runtime. |
| Reference audit loop | Process | openclaw, Octogent | Pull/fetch safe, dirty skip, remote quarantine, source freshness avant audit. |

## Priorités d'intégration

| Priorité | Ajouts | Raison |
| --- | --- | --- |
| P0 - rendre le standard opérable | Workflow State Engine, Knowledge Base Indexer, Advanced Context Orchestrator, Evidence-Gated Workflow FSM, Agent Telemetry Plane, Tool Blast-Radius Limiter | Sans ces briques, la structure reste conversationnelle, non spécialisée et difficile à auditer. |
| P1 - rendre le système maintenable | LLM Provider Abstraction, Capability Marketplace, Skill/Capability lifecycle, MCP Trust Gate, Memory Integrity Validator, Prompt/version observability, Guardrail Contract | Stabilise providers, capacités, sources, outils, prompts, mémoire et contrôles dans le temps. |
| P2 - rendre l'exécution robuste | Agent Backend Boundary, Local Agent Worker Pool, Runtime Provider Contract, Workspace Isolation, Browser Tool Contract, Trajectory Logging | Permet l'exécution multi-agent fiable dans workspace, IDE, navigateur et runtimes interchangeables. |
| P3 - production / infra | Kubernetes Agent Control Plane, Cluster Action Dry-run, Policy by Environment, Session Reliability SLO Reporter | Réservé aux déploiements multi-tenant, environnements sensibles, ops ou infra. |
| P4 - optimisation / sophistication | LLM Cost Registry, Doc-to-Graph Pipeline, Flow DSL minimal, Knowledge Narrative Packaging | Réduit coût, dette documentaire et complexité ; ajoute des capacités avancées non indispensables au socle. |

## Échelle de maturité opérable

Le statut `Fait socle` signifie que le pattern ou contrat est présent dans le référentiel, relié aux matrices et doté d'un modèle minimal. Il ne signifie pas automatiquement qu'une implémentation produit existe déjà.

| Statut opérable | Sens | Preuve attendue |
| --- | --- | --- |
| Documenté | Le concept est décrit avec intention, problème, solution, contrôles et anti-pattern. | entrée de pattern ou page dédiée. |
| Template disponible | Un modèle opérationnel réutilisable existe. | fichier dans `docs/modeles/`. |
| Exemple fourni | Un exemple rempli montre comment l'appliquer. | fichier dans `docs/modeles/exemples/`. |
| Vérifiable | Le pattern est relié à exigences, risques, preuves et télémétrie. | matrices mises à jour. |
| Prêt implémentation | Un utilisateur sait par quel profil commencer et quel artefact remplir. | parcours d'implémentation + maturité. |

## Documents à créer ou compléter

| Document | Action | Contenu attendu |
| --- | --- | --- |
| `docs/modele-reference-structure-agentique.md` | Ajuster | Ajouter les composants workflow engine, knowledge base indexer, runtime provider, capability registry, telemetry plane et visual evidence. |
| `docs/patterns/README.md` | Ajuster | Indexer tous les nouveaux patterns par famille et maturité. |
| `docs/parcours-implementation-agentique.md` | Créer | Donner un chemin minimal et progressif pour adopter le standard sans tout appliquer. |
| `docs/patterns/matrice-maturite-patterns.md` | Créer | Relier chaque pattern à son profil d'entrée minimal/contrôlé/orchestré/gouverné/production. |
| `docs/patterns/02-orchestration-contexte/README.md` | Compléter | Workflow State Engine, human interrupt, source graph, context constitution, compression gate. |
| `docs/patterns/03-gouvernance-controles/README.md` | Compléter | Prompt injection firewall, MCP trust, remote hygiene, guardrail contract, privilege boundary. |
| `docs/patterns/04-preuves-qualite/README.md` | Compléter | Evidence-gated FSM, visual evidence, eval lifecycle, cost/reliability SLO. |
| `docs/patterns/05-memoire-connaissances/README.md` | Compléter | Knowledge Base Indexer, memory palace, memory routing, contradiction detection, source quarantine. |
| `docs/patterns/06-runtime-evolution/README.md` | Compléter | Runtime provider, local worker pool, K8s control plane, orders dispatcher, primitive-first capabilities. |
| `docs/contrats-operationnels-agentiques.md` | Compléter | Ajouter tous les nouveaux contrats : workflow state, runtime provider, skill record, guardrail, browser tool, eval dataset. |
| `docs/observabilite-telemetrie-agentique.md` | Compléter | Ajouter trajectories, prompt versioning, eval dataset, cost, release telemetry, privacy model. |
| `docs/matrice-risques-controles-preuves.md` | Compléter | Mapper chaque nouveau contrôle à risque, preuve, métrique et niveau de conformité. |
| `diagrammes/schema-ideal-reference-agentique.mmd` | Ajuster | Montrer les nouvelles couches sans surcharger : workflow, context, runtime, telemetry, evidence. |
| `docs/references-agentiques.md` | Compléter | Ajouter un résumé des apports par projet et liens vers analyses. |

## Modèles opérationnels à ajouter

| Modèle | Sources | Usage |
| --- | --- | --- |
| `workflow-state-manifest.md` | LangGraph, Conductor, Dify, Langflow | Décrire graphes, états, transitions, retries, compensation et preuves. |
| `runtime-provider-contract.md` | OpenHands, agent-sandbox, gascity, kagent | Uniformiser local, subprocess, tmux, ACP, Kubernetes. |
| `capability-pack.md` | claude-skills, agent-skills, superpowers, gascity-packs | Déclarer capacité, permissions, tests, owner, version et runtime. |
| `skill-record.md` | claude-skills, Andrej Karpathy skills | Décrire activation, inputs, outputs, limites, exemples, tests. |
| `guardrail-contract.md` | OpenAI Agents SDK, kagent, LLMSecurityGuide | Définir input/output guardrails, décisions, métriques, incident. |
| `browser-tool-contract.md` | browser-use, pixel-agents, OpenHands | Définir scope URL, DOM, capture, actions, preuve et risques. |
| `eval-dataset-record.md` | Langfuse, Haystack, OpenAI Agents SDK | Versionner cas d'évaluation, expected, juge, seuil, historique. |
| `source-graph-record.md` | CodeGraphContext, graphify | Décrire nœuds, relations, provenance, fraîcheur, contradictions. |
| `knowledge-source-index.md` | Haystack, Dify, Langflow, CodeGraphContext | Décrire une source externe greffée : type, connecteur, ACL, index, fraîcheur, stratégie de réindexation. |
| `memory-routing-policy.md` | mempalace, graphify, VS Code Copilot Chat | Définir L0-L3, promotion, rappel, confiance et purge. |
| `llm-provider-registry.md` | OpenAI Agents SDK, VS Code Copilot Chat, Copilot, Codex, Claude, Gemini | Décrire providers, adapters, modèles, capacités, policies, evals, coûts et fallback. |

## Features à intégrer dans le produit documentaire

| Feature | Description | Statut recommandé |
| --- | --- | --- |
| Catalogue des bases de connaissance | Table des corpus greffés : repo, URL, API, MCP, DB, dossier, owner, ACL, fraîcheur, index. | Exemple fourni via `knowledge-source-repo-produit`. |
| Matrice projet -> pattern | Table reliant chaque projet source aux patterns récupérés. | Couvert par le plan global et la roadmap d'audit ; à industrialiser si produit dédié. |
| Heatmap de maturité | Visualiser quels patterns appartiennent aux profils minimal à mature. | Fait socle via `patterns/matrice-maturite-patterns.md`. |
| Diagramme des dépendances entre patterns | Montrer quels patterns contrôlent ou renforcent les autres. | Enrichi via `patterns/relations-patterns.md`. |
| Catalogue des anti-patterns issus des références | Exemples : agent sans preuve, RAG vérité, skill proliférante, outil sans blast-radius. | Couvert par les anti-patterns de chaque pattern ; catalogue transversal à enrichir ensuite. |
| Checklist d'intégration d'un nouveau projet de référence | Pull safe, dirty skip, diagramme, features, plan de récupération, merge global. | Couvert dans la roadmap d'audit ; à extraire en checklist produit si besoin. |
| Evidence profile par type de tâche | Code, UI, infra, docs, recherche, sécurité, modèle. | Fait socle via `profils-preuves-par-tache.md`. |
| Runbook de promotion d'une capacité | Draft -> expérimental -> canary -> enforced -> deprecated. | Exemple fourni via capability pack et RUN-07. |

## Arbitrages à conserver

| Tension | Arbitrage |
| --- | --- |
| Graphe durable vs simplicité | Le graphe durable devient obligatoire seulement à partir du profil orchestré/gouverné. |
| Visual builder vs standard textuel | Accepté si un manifest exportable et auditable existe. |
| Mémoire riche vs source de vérité | Mémoire et vecteurs aident le rappel ; la source active reste prioritaire. |
| Autonomie vs validation | Autonomie graduée par risque, preuve, coût, réversibilité et validation authority. |
| Observabilité riche vs confidentialité | Traces corrélées mais minimisées, masquées et gouvernées par rétention. |
| Marketplace vs prolifération | Toute capacité a owner, statut, tests, expiration et preuve d'usage. |
| Runtime local vs production | Local worker pool pour tâches courtes ; K8s control plane pour production multi-tenant. |
| Agents spécialisés vs core monolithique | Agent backend boundary obligatoire dès qu'il y a tools, events, plugins ou sandbox. |

## Ordre recommandé d'exécution

1. Stabiliser le modèle de référence : composants, profils, interfaces et cycle de fonctionnement.
2. Compléter le catalogue de patterns par famille avec les nouveaux patterns P0/P1.
3. Ajouter les modèles opérationnels manquants et les relier dans `contrats-operationnels-agentiques.md`.
4. Mettre à jour matrices risques/contrôles/preuves et patterns/exigences/preuves.
5. Mettre à jour les diagrammes Mermaid de famille et le schéma idéal.
6. Ajouter les features documentaires : matrice projet->pattern, heatmap maturité, checklist nouveau projet de référence.
7. Repasser une validation de cohérence : liens Markdown, index patterns, modèles référencés, diagrammes existants.

## Matrice ADD actionnable

Tous les items ci-dessous sont au minimum au statut opérable `Documenté`. Les items disposant d'un modèle opérationnel et d'un exemple rempli atteignent `Template disponible` ou `Exemple fourni`. Les matrices risques/preuves/relations donnent le niveau `Vérifiable`.

| ID | Ajout | Type | Priorité | État actuel | Dépend de | Documents impactés | Critère Done |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADD-001 | Workflow State Engine | Pattern central | P0 | Fait socle | Aucun | `patterns/02-orchestration-contexte`, `modele-reference`, `contrats-operationnels`, diagrammes | États, transitions, retries, interruptions, preuves et modèle `workflow-state-manifest` définis. |
| ADD-002 | Knowledge Base Indexer | Pattern connaissance | P0 | Fait socle | Aucun | `patterns/05-memoire-connaissances`, `gouvernance-modeles-et-connaissances`, `memoire-hybride`, `orchestration-contexte`, modèles | Distinction claire mémoire/contexte/base de connaissance + connecteurs + ACL + index + réindexation documentés. |
| ADD-003 | Advanced Context Orchestrator | Pattern contexte | P0 | Fait socle | ADD-002 | `orchestration-contexte`, `patterns/02`, `context-pack` | Le contexte consomme la base de connaissance via retrieval contrôlé sans la confondre avec mémoire ou source de vérité. |
| ADD-004 | Evidence-Gated Workflow FSM | Pattern qualité | P0 | Fait socle | ADD-001 | `patterns/04`, `ledger-preuves`, `verification-verdict` | Chaque transition majeure a preuve attendue, verdict et réponse si preuve absente. |
| ADD-005 | Agent Telemetry Plane | Pattern observabilité | P0 | Fait socle | ADD-001 | `observabilite-telemetrie`, `observabilite-evals-slo`, diagrammes | Spans, métriques, events, coûts, evals et SLO minimaux documentés. |
| ADD-006 | Tool Blast-Radius Limiter | Contrôle | P0 | Fait socle | Aucun | `patterns/03`, `garde-fous`, `matrice-risques-controles-preuves` | Scopes fichiers/réseau/shell/browser/prod/coût définis et mappés aux preuves. |
| ADD-007 | Capability Marketplace | Pattern runtime | P1 | Fait socle | Aucun | `patterns/06`, `profils-capacites`, modèles | Capacité = owner, statut, permissions, tests, version, expiration, preuve d'usage. |
| ADD-008 | Skill/Capability lifecycle | Lifecycle | P1 | Fait socle | ADD-007 | `patterns/06`, `profils-capacites`, `patterns/lifecycle-maturite-patterns` | Cycle draft -> experimental -> canary -> enforced -> deprecated/retired documenté avec preuves. |
| ADD-009 | MCP Trust Gate | Contrôle | P1 | Fait socle | ADD-006 | `contrat-mcp`, `patterns/03`, matrice risques | Origine, permissions, env vars, capabilities et blast-radius MCP vérifiés. |
| ADD-010 | Memory Integrity Validator | Contrôle mémoire | P1 | Fait socle | ADD-002 | `patterns/05`, `memoire-hybride`, `gouvernance-modeles-et-connaissances` | Contamination, obsolescence, contradictions et désindexation ont des réponses documentées. |
| ADD-011 | LLM Provider Abstraction | Contrat modèle | P1 | Fait socle | ADD-005 | `gouvernance-modeles-et-connaissances`, `routage-llm-retention-connaissances`, `politique-routage-llm`, diagrammes | Provider registry, adapters, capacités, policies, statuts, evals et fallback multi-provider documentés. |
| ADD-012 | Prompt/version observability | Feature observabilité | P1 | Fait socle | ADD-005, ADD-011 | `observabilite-telemetrie`, `observabilite-evals-slo`, `politique-routage-llm` | Prompts versionnés, datasets/evals liés, rollbacks et régressions traçables par provider/modèle. |
| ADD-013 | Guardrail Contract | Contrat contrôle | P1 | Fait socle | ADD-006 | `contrats-operationnels`, `patterns/03`, `garde-fous`, modèles | Input/output guardrails, décisions, fallback, preuve et incident documentés. |
| ADD-014 | Agent Backend Boundary | Pattern runtime | P2 | Fait socle | ADD-001 | `patterns/06`, `runtime-agentique`, `contrats-formels` | Séparation workflow node / backend agent / events / tools / sandbox explicitée. |
| ADD-015 | Local Agent Worker Pool | Pattern runtime | P2 | Fait socle | ADD-014 | `patterns/06`, `runtime-agentique`, diagrammes | Slots, queue, cancellation, retry, health, telemetry et preuves définis. |
| ADD-016 | Runtime Provider Contract | Contrat runtime | P2 | Fait socle | ADD-014 | `contrats-operationnels`, `runtime-agentique`, modèles | Contrat commun local/subprocess/tmux/ACP/K8s : lifecycle, exec, logs, ressources, health. |
| ADD-017 | Workspace Isolation | Contrôle runtime | P2 | Fait socle | ADD-006 | `runtime-agentique`, `patterns/03`, `matrice-risques-controles-preuves` | Workspace root, fichiers autorisés, réseau, secrets, teardown et preuves définis. |
| ADD-018 | Browser Tool Contract | Contrat outil | P2 | Fait socle | ADD-006 | `contrats-operationnels`, `patterns/04`, modèles | Scope URL, DOM, screenshot, action, preuve visuelle et risque documentés. |
| ADD-019 | Trajectory Logging | Feature observabilité | P2 | Fait socle | ADD-005 | `observabilite-telemetrie`, `ledger-preuves`, `runtime-agentique` | Trajectoire agent état -> action -> observation -> décision -> preuve journalisée. |
| ADD-020 | Kubernetes Agent Control Plane | Profil production | P3 | Fait socle | ADD-016 | `patterns/06`, `runtime-agentique`, `matrice-risques` | Provider, quotas, service accounts, policies, network allowlists et OTel définis. |
| ADD-021 | Cluster Action Dry-run | Contrôle infra | P3 | Fait socle | ADD-020 | `simulation-pre-execution`, `patterns/03`, `matrice-risques-controles-preuves` | Toute action cluster produit plan, impact, policy decision, rollback et go/no-go. |
| ADD-022 | Policy by Environment | Contrôle infra | P3 | Fait socle | ADD-006 | `garde-fous`, `runtime-agentique`, `matrice-risques-controles-preuves` | Règles distinctes local/staging/prod avec données, réseau, secrets et validation authority. |
| ADD-023 | Session Reliability SLO Reporter | SLO runtime | P3 | Fait socle | ADD-005 | `observabilite-evals-slo`, `observabilite-telemetrie`, modèles | CrashRate, UnhealthyRate, idle kills, quarantines et drains par model/rig suivis. |
| ADD-024 | LLM Cost Registry | Feature observabilité | P4 | Fait socle | ADD-005, ADD-011 | `observabilite-telemetrie`, `politique-routage-llm`, modèles | Coûts provider/modèle/rig reliés aux traces, budgets et fallback. |
| ADD-025 | Doc-to-Graph Pipeline | Feature connaissance | P4 | Fait socle | ADD-002 | `patterns/05`, `references-agentiques`, futures features docs | Docs/patterns convertibles en graphe avec provenance, relations et contradictions. |
| ADD-026 | Flow DSL minimal | Feature orchestration | P4 | Fait socle | ADD-001 | `patterns/02`, `contrats-operationnels`, modèles | DSL simple pour workflows légers, validable et exportable sans moteur lourd. |
| ADD-027 | Knowledge Narrative Packaging | Feature connaissance | P4 | Fait socle | ADD-002 | `patterns/05`, `gouvernance-modeles-et-connaissances` | Storylines de domaine utilisables comme couche pédagogique, jamais comme source de vérité. |
