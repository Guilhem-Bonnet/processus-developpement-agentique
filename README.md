# Standard de structure agentique

Ce projet documente la base d'une structure agentique fonctionnelle, sous une forme proche d'un standard, d'un référentiel d'architecture et d'un catalogue de design patterns. L'agent devient l'entreprise opératrice et l'utilisateur devient le client. Le client apporte le besoin, le contexte métier, les arbitrages et l'acceptation. L'entreprise-agent organise la découverte, le cadrage, l'architecture, l'exécution, la qualité, la sécurité, la traçabilité et la livraison au moyen de prompts, skills, outils, MCP, hooks, mémoire, Kanban et subagents.

Cette documentation n'est pas un tutoriel ni un exemple d'implémentation. Elle définit les éléments constitutifs, exigences, interfaces, niveaux de conformité et patterns nécessaires pour concevoir une structure agentique gouvernable, vérifiable et maintenable.

## Contenu

- [Diagramme de décision agentique](docs/diagramme-decision-agentique.md)
- [Diagramme d'orchestration interne](docs/diagramme-orchestration-agentique.md)
- [Terminologie agentique](docs/terminologie-agentique.md)
- [Modèle de référence d'une structure agentique](docs/modele-reference-structure-agentique.md)
- [Exigences normatives d'une structure agentique](docs/exigences-normatives-structure-agentique.md)
- [Catalogue des patterns agentiques](docs/patterns/README.md)
- [Relations entre patterns agentiques](docs/patterns/relations-patterns.md)
- [Matrice patterns, exigences et preuves](docs/patterns/matrice-patterns-exigences-preuves.md)
- [Contrats formels agentiques](docs/patterns/contrats-formels-agentiques.md)
- [Lifecycle et maturité des patterns](docs/patterns/lifecycle-maturite-patterns.md)
- [Anti-patterns agentiques](docs/patterns/anti-patterns-agentiques.md)
- [Profils de capacités agentiques](docs/profils-capacites-agentiques.md)
- [Niveaux de conformité agentique](docs/niveaux-conformite-agentique.md)
- [Runtime agentique et surfaces gouvernées](docs/runtime-agentique-et-surfaces-gouvernees.md)
- [Ledger, preuves et verdicts agentiques](docs/ledger-preuves-verdicts-agentiques.md)
- [Mémoire hybride agentique](docs/memoire-hybride-agentique.md)
- [Matrice de preuves de conformité agentique](docs/matrice-preuves-conformite-agentique.md)
- [Cadre agent-utilisateur](docs/cadre-agent-utilisateur.md)
- [Architecture de pilotage agentique](docs/architecture-pilotage-agentique.md)
- [Orchestration du contexte agentique](docs/orchestration-contexte-agentique.md)
- [Gouvernance d'exécution agentique](docs/gouvernance-execution-agentique.md)
- [Défauts IA et fiabilité agentique](docs/defauts-ia-et-fiabilite.md)
- [Observabilité, evals et SLO agentiques](docs/observabilite-evals-slo-agentiques.md)
- [Simulation pré-exécution agentique](docs/simulation-pre-execution-agentique.md)
- [Incidents et reprise agentique](docs/incidents-et-reprise-agentique.md)
- [Gouvernance des modèles et des connaissances](docs/gouvernance-modeles-et-connaissances.md)
- [Routage LLM et rétention des connaissances](docs/routage-llm-retention-connaissances.md)
- [Contrats opérationnels agentiques](docs/contrats-operationnels-agentiques.md)
- [Prompts des subagents agentiques](docs/prompts-subagents-agentiques.md)
- [Questionnaires agentiques](docs/questionnaires-agentiques.md)
- [Garde-fous agentiques](docs/garde-fous-agentiques.md)
- [Références agentiques](docs/references-agentiques.md)
- [Modèle de brief agentique](docs/modeles/brief-agentique.md)
- [Modèles opérationnels agentiques](docs/contrats-operationnels-agentiques.md#templates-disponibles)
- [Source Mermaid du cycle](diagrammes/cycle-agentique.mmd)
- [Source Mermaid de l'orchestration](diagrammes/orchestration-agentique.mmd)
- [Source Mermaid de l'orchestration du contexte](diagrammes/orchestration-contexte-agentique.mmd)
- [Source Mermaid du routage et de la rétention](diagrammes/routage-retention-connaissances.mmd)
- [Source Mermaid du runtime agentique](diagrammes/runtime-surfaces-agentiques.mmd)
- [Source Mermaid du ledger de preuves](diagrammes/ledger-preuves-verdicts.mmd)
- [Source Mermaid de la mémoire hybride](diagrammes/memoire-hybride-agentique.mmd)
- [Source Mermaid des patterns organisationnels](diagrammes/patterns-organisation.mmd)
- [Source Mermaid des patterns d'orchestration et contexte](diagrammes/patterns-orchestration-contexte.mmd)
- [Source Mermaid des patterns de gouvernance](diagrammes/patterns-gouvernance-controles.mmd)
- [Source Mermaid des patterns de preuves et qualité](diagrammes/patterns-preuves-qualite.mmd)
- [Source Mermaid des patterns de mémoire et connaissances](diagrammes/patterns-memoire-connaissances.mmd)
- [Source Mermaid des patterns runtime et évolution](diagrammes/patterns-runtime-evolution.mmd)

## Principes

1. Le besoin client est la source de vérité, mais l'agent doit le transformer en exigences, critères d'acceptation, backlog et preuves.
2. L'agent ne doit pas compenser un besoin flou par de l'improvisation : il exploite d'abord le contexte disponible, puis pose des questions ciblées quand l'information n'est pas déductible.
3. L'entreprise-agent sépare les responsabilités : analyste besoin, architecte, développeur, QA, sécurité, ops, documentation, mémoire et orchestration.
4. Chaque action passe par des garde-fous adaptés au risque : permission, hook, sandbox, revue, test, évaluation, observation ou validation humaine.
5. Le contexte est géré comme une infrastructure : workspace et docs pour le réel, base vectorielle pour le rappel long terme, Redis pour le contexte chaud, journal de preuves pour la traçabilité.
6. La taille du contexte est pilotée par étape : chaque subagent reçoit un task envelope minimal et rend un handoff packet qui déclenche la suite.
7. Les outils sont gouvernés : prompts, skills, outils locaux, MCP, navigateur, terminal, dépôt distant et services externes ont des permissions explicites.
8. Les accès, validations et coûts de contexte sont explicites : une carte sait qui agit, avec quel droit, quel budget de tokens et quel validateur.
9. Les défauts natifs de l'IA sont traités comme des risques de conception : hallucination, surconfiance, oubli, complaisance, dérive de contexte et faux Done.
10. Les modèles, connaissances, mémoires et sources indexées ont un cycle de vie : routage LLM par tâche, évaluation, fallback, expiration, réindexation, désindexation et oubli.
11. Les actions risquées passent par une simulation pré-exécution et les incidents agentiques ont un processus de détection, rollback, correction et post-mortem.
12. Le travail est piloté comme un projet : Kanban, backlog, Definition of Ready, Definition of Done, priorités, dépendances, risques et décisions.
13. La qualité du livrable ne repose pas sur la confiance dans le modèle, mais sur des preuves : tests, lint, build, rendus, revues, evals, red teaming, logs, SLO et acceptation client.
14. Les runtimes agentiques ont leurs propres surfaces de contrôle et de sortie : agents, skills, hooks, workflows, preuves, traces et artefacts doivent être versionnés, audités, promus ou purgés.
15. La conformité agentique se prouve par des artefacts actifs : mission ledger, evidence packs, verification verdicts, registres, manifests, hooks, policies et dossiers d'acceptation.

## Nature du référentiel

| Aspect | Position |
| --- | --- |
| Type | standard documentaire, modèle de référence et catalogue de patterns. |
| But | définir la base commune d'une structure agentique qui fonctionne. |
| Non-but | imposer un fournisseur, un framework ou un runtime unique. |
| Vérification | exigences normatives, contrats, preuves et niveaux de conformité. |
| Évolution | les patterns, exigences et profils peuvent être versionnés comme un référentiel d'architecture. |
| Inspiration runtime | les patterns éprouvés par des runtimes réels peuvent enrichir le standard sans le rendre dépendant d'un outil. |

## Vision organisationnelle

| Client utilisateur | Entreprise-agent |
| --- | --- |
| Exprime le problème, les priorités, les contraintes et les critères d'acceptation. | Transforme la demande en mission qualifiée, exigences, plan, lots et preuves. |
| Valide les décisions métier, le risque acceptable et le livrable final. | Orchestre subagents, outils, mémoire, Kanban, hooks et validations. |
| Fournit les informations non déductibles et les accès nécessaires. | Exploite le contexte réel avant de solliciter le client. |
| Autorise les actions coûteuses, sensibles ou irréversibles. | Bloque ou escalade les actions qui dépassent le périmètre ou la politique. |

## Différence avec la version humaine

| Version humaine | Version agentique fusionnée |
| --- | --- |
| Organise les étapes d'un projet de développement classique. | Organise le même projet avec une entreprise-agent qui internalise des rôles et outils. |
| Met l'accent sur produit, design, dev, QA, ops et sécurité. | Ajoute orchestration, prompts, skills, subagents, MCP, hooks, mémoire et contexte. |
| Valide le livrable par exigences, tests, review et acceptance. | Valide aussi les actions autonomes, les sources de contexte, les outils et la fiabilité IA. |
| Suit le backlog et les livraisons. | Suit aussi les traces d'agent, décisions, risques IA, evals, red teaming et mémoire. |

## Références structurantes

La base s'appuie sur ISO/IEC/IEEE 29148, ISO/IEC/IEEE 42010, ISO/IEC 25010, NIST SSDF, OWASP ASVS, WCAG, OpenAPI, Docker, GitHub Actions, DORA, NIST AI RMF, ISO/IEC 42001, OWASP GenAI Security Project, OWASP Top 10 for LLM Applications, Model Context Protocol, OpenAI Agents SDK, Claude Code documentation, GitHub Copilot Docs, GitHub Projects, Redis vector search, Qdrant et OpenTelemetry.
