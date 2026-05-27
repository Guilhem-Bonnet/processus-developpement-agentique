# Catalogue des patterns agentiques

Ce dossier classe les patterns de structure agentique par famille. Le but est de rendre le référentiel lisible comme un catalogue de design patterns : chaque famille regroupe les problèmes récurrents, les solutions stables, les contrats attendus et les contrôles de conformité.

## Règle de classement

Un pattern est classé selon la responsabilité principale qu'il porte. S'il touche plusieurs familles, il est référencé depuis la famille secondaire, mais défini une seule fois pour éviter les doublons normatifs.

## Documents transversaux

| Document | Usage |
| --- | --- |
| [Relations entre patterns](relations-patterns.md) | Visualiser dépendances, contrôles et renforcements entre patterns. |
| [Lifecycle et maturité des patterns](lifecycle-maturite-patterns.md) | Définir statut, niveau de conformité et promotion d'un pattern. |
| [Matrice de maturité des patterns](matrice-maturite-patterns.md) | Savoir à partir de quel profil appliquer chaque pattern. |
| [Parcours d'implémentation agentique](../parcours-implementation-agentique.md) | Démarrer avec un sous-ensemble réaliste avant le standard complet. |
| [Contrats formels agentiques](contrats-formels-agentiques.md) | Normaliser les schémas minimaux des interfaces agentiques. |
| [Matrice patterns, exigences et preuves](matrice-patterns-exigences-preuves.md) | Relier chaque famille de patterns aux exigences et preuves attendues. |
| [Anti-patterns agentiques](anti-patterns-agentiques.md) | Décrire les mauvaises formes récurrentes et leurs remédiations. |

## Hiérarchie des patterns

| Rang | Type | Rôle |
| --- | --- | --- |
| 1 | Fondation | Définit les principes sans lesquels le système n'est pas gouvernable. |
| 2 | Exécution | Organise le travail, les délégations et les transitions. |
| 3 | Contrôle | Autorise, bloque, simule ou escalade les actions. |
| 4 | Preuve | Rend les décisions vérifiables et auditables. |
| 5 | Mémoire | Gère rappel, vérité, rétention, correction et oubli. |
| 6 | Évolution | Encadre les artefacts dynamiques et le cycle de vie runtime. |

| Famille | Dossier | Responsabilité principale |
| --- | --- | --- |
| Organisation | [01-organisation](01-organisation/README.md) | Rôles, autorités, relation client / entreprise-agent. |
| Orchestration et contexte | [02-orchestration-contexte](02-orchestration-contexte/README.md) | Délégation, paquets de contexte, subagents, orchestration contextuelle. |
| Gouvernance et contrôles | [03-gouvernance-controles](03-gouvernance-controles/README.md) | Hooks, politiques, simulations, blocages et validations préventives. |
| Preuves et qualité | [04-preuves-qualite](04-preuves-qualite/README.md) | Vérification, observabilité, ledgers et verdicts. |
| Mémoire et connaissances | [05-memoire-connaissances](05-memoire-connaissances/README.md) | Mémoire hybride, rétention, nettoyage et dérive documentaire. |
| Runtime et évolution | [06-runtime-evolution](06-runtime-evolution/README.md) | Artefacts dynamiques, surfaces runtime, cycles de vie des capacités. |

## Index des patterns

| ID | Pattern | Famille |
| --- | --- | --- |
| ORG-01 | Entreprise-agent | Organisation |
| ORG-02 | Validation authority | Organisation |
| ORC-01 | Orchestrateur et subagents spécialisés | Orchestration et contexte |
| ORC-02 | Task envelope | Orchestration et contexte |
| ORC-03 | Handoff packet | Orchestration et contexte |
| ORC-04 | Context router | Orchestration et contexte |
| ORC-05 | Orchestrateur de contexte avancé | Orchestration et contexte |
| ORC-06 | Context constitution | Orchestration et contexte |
| ORC-07 | Context conflict resolver | Orchestration et contexte |
| ORC-08 | Context budget escalation | Orchestration et contexte |
| ORC-09 | Workflow State Engine | Orchestration et contexte |
| ORC-10 | Flow DSL minimal | Orchestration et contexte |
| GOV-01 | Policy engine et hooks | Gouvernance et contrôles |
| GOV-02 | Dry-run avant action risquée | Gouvernance et contrôles |
| GOV-03 | Hook lifecycle progressif | Gouvernance et contrôles |
| GOV-04 | Autonomie gouvernée | Gouvernance et contrôles |
| GOV-05 | Agent privilege boundary | Gouvernance et contrôles |
| GOV-06 | Merge lane fault classifier | Gouvernance et contrôles |
| GOV-07 | Tool blast-radius limiter | Gouvernance et contrôles |
| GOV-08 | Guardrail contract | Gouvernance et contrôles |
| GOV-09 | MCP Trust Gate | Gouvernance et contrôles |
| GOV-10 | Policy by environment | Gouvernance et contrôles |
| GOV-11 | Cluster action dry-run | Gouvernance et contrôles |
| GOV-12 | Prompt Injection Firewall | Gouvernance et contrôles |
| GOV-13 | Remote Hygiene Guard | Gouvernance et contrôles |
| GOV-14 | Decision Council Gate | Gouvernance et contrôles |
| QUA-01 | Claim ledger | Preuves et qualité |
| QUA-02 | Observabilité agentique | Preuves et qualité |
| QUA-03 | Mission ledger append-only | Preuves et qualité |
| QUA-04 | Evidence pack et verification verdict | Preuves et qualité |
| QUA-05 | Evidence-driven transition | Preuves et qualité |
| QUA-06 | LLM cost registry | Preuves et qualité |
| QUA-07 | Session reliability SLO reporter | Preuves et qualité |
| QUA-08 | Agent telemetry plane | Preuves et qualité |
| QUA-09 | Prompt/version observability | Preuves et qualité |
| QUA-10 | Trajectory logging | Preuves et qualité |
| QUA-11 | Browser evidence contract | Preuves et qualité |
| QUA-12 | Visual Evidence Pack | Preuves et qualité |
| QUA-13 | Eval lifecycle | Preuves et qualité |
| KNO-01 | Knowledge janitor | Mémoire et connaissances |
| KNO-02 | Mémoire hybride | Mémoire et connaissances |
| KNO-03 | Doc drift detector | Mémoire et connaissances |
| KNO-04 | Knowledge promotion | Mémoire et connaissances |
| KNO-05 | Memory contamination response | Mémoire et connaissances |
| KNO-06 | Knowledge Base Indexer | Mémoire et connaissances |
| KNO-07 | Memory integrity validator | Mémoire et connaissances |
| KNO-08 | Doc-to-graph pipeline | Mémoire et connaissances |
| KNO-09 | Knowledge narrative packaging | Mémoire et connaissances |
| KNO-10 | Source Graph Resolver | Mémoire et connaissances |
| MOD-01 | Model router | Gouvernance et contrôles |
| MOD-02 | Model retirement guard | Gouvernance et contrôles |
| RUN-01 | Dynamic factory contrôlée | Runtime et évolution |
| RUN-02 | Runtime output governance | Runtime et évolution |
| RUN-03 | Kubernetes agent control plane | Runtime et évolution |
| RUN-04 | Orders exec/formula dispatcher | Runtime et évolution |
| RUN-05 | Primitive-first capability model | Runtime et évolution |
| RUN-06 | Capability marketplace | Runtime et évolution |
| RUN-07 | Skill/capability lifecycle | Runtime et évolution |
| RUN-08 | Runtime provider contract | Runtime et évolution |
| RUN-09 | Agent backend boundary | Runtime et évolution |
| RUN-10 | Local agent worker pool | Runtime et évolution |
| RUN-11 | Workspace isolation | Runtime et évolution |
| RUN-12 | Secure local coordinator | Runtime et évolution |

## Format attendu d'un pattern

| Élément | Description |
| --- | --- |
| Intention | Ce que le pattern cherche à obtenir. |
| Problème | Le risque ou défaut récurrent qu'il corrige. |
| Solution | Le mécanisme structurel attendu. |
| Contrôles | Les preuves, hooks, registres ou validations nécessaires. |
| Anti-pattern | La forme dangereuse ou immature à éviter. |

## Usage normatif

Les patterns ne remplacent pas les exigences normatives. Ils expliquent comment satisfaire les exigences de manière réutilisable. Une implémentation peut adapter les noms et outils, mais elle doit conserver les responsabilités, contrats et contrôles si elle revendique le même niveau de conformité.
