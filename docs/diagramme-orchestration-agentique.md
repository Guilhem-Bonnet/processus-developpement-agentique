# Diagramme d'orchestration agentique

Ce diagramme montre le niveau inférieur : comment l'entreprise-agent transforme une demande client en exécution contrôlée. Il ne décrit pas un produit particulier, mais une architecture de pilotage réutilisable pour agents outillés.

```mermaid
flowchart LR
    CLIENT([Client utilisateur]) --> INTAKE["Interface de mission<br/>brief, contraintes, validation"]
    INTAKE --> ORCH["Orchestrateur entreprise-agent<br/>priorise, delegue, synthese"]

    subgraph GOV["Gouvernance"]
        POLICY["Policy engine<br/>permissions, donnees, cout, risque"]
        FAILURE["Failure mode registry<br/>hallucination, biais, faux Done"]
        ACCESS["Access control<br/>roles, scopes, secrets"]
        HOOKS["Hooks<br/>pre-action, pre-tool, post-tool, pre-write, pre-release"]
        APPROVAL["Validation humaine<br/>decisions sensibles"]
        VALIDAUTH["Autorite de validation<br/>client, QA, securite, ops"]
    end

    subgraph CTX["Context engineering"]
        ROUTER["Context router<br/>selection, fraicheur, confiance"]
        WORKSPACE["Workspace et docs<br/>code, tests, ADR, erreurs"]
        VECTOR["Base vectorielle<br/>memoire longue, RAG, similarite"]
        REDIS["Redis contexte chaud<br/>session, cache semantique, etat court"]
        JANITOR["Knowledge janitor<br/>retention, archive, desindexation, purge"]
        EVIDENCE["Journal de preuves<br/>sources, commandes, resultats"]
    end

    subgraph COL["Context orchestration layer"]
        STAGE["Etape courante<br/>mission, risque, DoR"]
        PROFILE["Profil de contexte<br/>role, budget, sources"]
        TOKEN["Token economy<br/>budget, cache, compression"]
        ENVELOPE["Task envelope<br/>objectif, contexte minimal, outils, sortie"]
        HANDOFF["Handoff packet<br/>preuves, hypotheses, risques, trigger"]
    end

    subgraph CAP["Capacites agentiques"]
        PROMPTS["Prompts et instructions<br/>contrats de comportement"]
        MODEL["LLM router<br/>tache, modele, fallback, evals"]
        SKILLS["Skills<br/>procedures reutilisables"]
        MCP["Passerelle MCP<br/>outils, donnees, workflows"]
        TOOLS["Outils locaux et externes<br/>edition, terminal, navigateur, CI"]
    end

    subgraph TEAM["Subagents specialises"]
        ANALYST["Analyste besoin"]
        ARCH["Architecte"]
        DESIGN["Design UI/UX et DA"]
        DEV["Developpeur"]
        QA["QA et evals"]
        SEC["Securite"]
        CRITIC["Critique et red team"]
        OPS["Ops et livraison"]
        DOC["Documentation"]
    end

    subgraph FLOW["Pilotage livraison"]
        KANBAN["Kanban<br/>backlog, pret, en cours, verification, accepte"]
        DRYRUN["Dry-run<br/>impact, permissions, rollback"]
        CHECKS["Quality gates<br/>tests, lint, build, scans, red teaming"]
        REVIEWS["Revues croisees<br/>pair, QA, client"]
        EVALS["Evals et SLO<br/>scorecards, couts, qualite"]
        INCIDENT["Incident response<br/>stop, rollback, post-mortem"]
        OBS["Observabilite<br/>traces, metriques, logs, couts"]
        DELIVERY["Dossier de livraison<br/>diff, preuves, limites, decisions"]
    end

    ORCH --> POLICY
    POLICY --> FAILURE
    FAILURE --> ACCESS
    ACCESS --> HOOKS
    HOOKS --> APPROVAL
    APPROVAL --> VALIDAUTH
    VALIDAUTH --> ORCH

    ORCH --> STAGE
    STAGE --> PROFILE
    PROFILE --> TOKEN
    TOKEN --> ROUTER
    ROUTER --> WORKSPACE
    ROUTER --> VECTOR
    ROUTER --> REDIS
    ROUTER --> JANITOR
    ROUTER --> ENVELOPE
    ROUTER --> EVIDENCE
    JANITOR --> VECTOR
    JANITOR --> REDIS
    EVIDENCE --> ORCH

    ORCH --> MODEL
    MODEL --> PROMPTS
    ORCH --> SKILLS
    ORCH --> MCP
    MCP --> TOOLS
    TOOLS --> HOOKS

    ORCH --> KANBAN
    KANBAN --> DRYRUN
    DRYRUN --> ENVELOPE
    ENVELOPE --> ANALYST
    ENVELOPE --> ARCH
    ENVELOPE --> DESIGN
    ENVELOPE --> DEV
    ENVELOPE --> QA
    ENVELOPE --> SEC
    ENVELOPE --> CRITIC
    ENVELOPE --> OPS
    ENVELOPE --> DOC

    ANALYST --> HANDOFF
    ARCH --> HANDOFF
    DESIGN --> HANDOFF
    DEV --> CHECKS
    QA --> CHECKS
    SEC --> CHECKS
    CRITIC --> REVIEWS
    OPS --> OBS
    DOC --> DELIVERY
    CHECKS --> REVIEWS
    REVIEWS --> HANDOFF
    REVIEWS --> EVALS
    EVALS --> INCIDENT
    INCIDENT --> ORCH
    OBS --> HANDOFF
    HANDOFF --> EVIDENCE

    CHECKS --> EVIDENCE
    REVIEWS --> DELIVERY
    EVALS --> EVIDENCE
    OBS --> EVIDENCE
    CHECKS --> DELIVERY
    DELIVERY --> CLIENT
```

La source autonome est disponible dans [../diagrammes/orchestration-agentique.mmd](../diagrammes/orchestration-agentique.mmd). Les règles opérables sont détaillées dans [gouvernance-execution-agentique.md](gouvernance-execution-agentique.md), les prompts de rôle dans [prompts-subagents-agentiques.md](prompts-subagents-agentiques.md) et les modes d'échec IA dans [defauts-ia-et-fiabilite.md](defauts-ia-et-fiabilite.md).

## Lecture rapide

| Bloc | Rôle |
| --- | --- |
| Interface de mission | Capture le besoin client, les contraintes, les validations attendues et les permissions. |
| Orchestrateur | Décide quoi traiter, quoi déléguer, quoi vérifier et quoi restituer. |
| Gouvernance | Empêche les actions hors périmètre, risquées, coûteuses ou non autorisées, avec accès, validateurs et défauts IA explicites. |
| Context engineering | Sélectionne les sources utiles, sépare contexte chaud et mémoire longue, nettoie les connaissances obsolètes et trace les preuves. |
| Context orchestration layer | Adapte la taille du contexte à l'étape, économise les tokens, prépare les task envelopes et contrôle les handoff packets. |
| Capacités agentiques | Fournit instructions, routage LLM par tâche, workflows, outils et connecteurs externes. |
| Subagents | Isolent les travaux spécialisés, y compris design/DA et critique/red-team, et réduisent la pollution du contexte principal. |
| Pilotage livraison | Rend le travail visible, vérifiable, priorisé et acceptable par le client avec dry-run, revues, evals, SLO et reprise incident. |

## Intention du niveau inférieur

Le diagramme rend explicite que la fiabilité ne vient pas d'un agent unique qui sait tout. Elle vient d'un système de contrôle : rôles spécialisés, contexte sourcé, outils permissionnés, hooks, preuves, évaluations, traçabilité et validation client.
