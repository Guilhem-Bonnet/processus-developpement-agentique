# Références agentiques

Cette page liste les références utiles pour cadrer le travail d'une entreprise-agent et de son client. Les normes ISO/IEC/IEEE sont référencées par leurs pages officielles sans reproduire leur contenu normatif.

## Gouvernance IA et sécurité agentique

| Domaine | Référence | Nature | Usage dans le processus |
| --- | --- | --- | --- |
| Gestion du risque IA | [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) | Cadre NIST | Gouverner, cartographier, mesurer et gérer les risques IA. |
| IA générative | [NIST AI RMF Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1) | Profil NIST | Identifier les risques propres aux systèmes GenAI : hallucination, abus, données, intégrité. |
| Management des systèmes IA | [ISO/IEC 42001:2023](https://www.iso.org/standard/81230.html) | Norme internationale | Mettre en place un système de management IA responsable et améliorable. |
| Sécurité GenAI | [OWASP GenAI Security Project](https://genai.owasp.org/) | Projet OWASP | Structurer la sécurité des systèmes GenAI et agentiques. |
| Risques LLM | [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) | Guide OWASP | Prompt injection, exposition de données, supply chain, actions excessives, etc. |
| Développement sécurisé | [NIST SP 800-218 SSDF](https://csrc.nist.gov/pubs/sp/800/218/final) | Recommandation NIST | Structurer les pratiques de développement sécurisé et supply chain. |
| Vérification sécurité | [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/) | Standard OWASP | Définir des exigences de sécurité applicative vérifiables. |

## Agents, prompts, tools, hooks et subagents

| Domaine | Référence | Nature | Usage dans le processus |
| --- | --- | --- | --- |
| Agents en code | [OpenAI Agents SDK](https://developers.openai.com/api/docs/guides/agents) | Documentation officielle | Concevoir agents qui planifient, appellent des outils, collaborent et maintiennent l'état. |
| Guardrails et validation | [OpenAI Agents SDK - Guardrails](https://developers.openai.com/api/docs/guides/agents/guardrails-approvals) | Documentation officielle | Ajouter validation, approbation humaine et blocage avant actions risquées. |
| Évaluation agents | [OpenAI - Evaluate agent workflows](https://developers.openai.com/api/docs/guides/agent-evals) | Documentation officielle | Tester workflows agentiques sur cas représentatifs. |
| Outils et MCP | [OpenAI - Tools, MCP and connectors](https://developers.openai.com/api/docs/guides/tools-connectors-mcp) | Documentation officielle | Connecter agents à outils, connecteurs et MCP. |
| Subagents | [Claude Code - Create custom subagents](https://code.claude.com/docs/en/sub-agents) | Documentation officielle | Isoler contexte, spécialiser les rôles, limiter outils et permissions. |
| Hooks | [Claude Code - Hooks reference](https://code.claude.com/docs/en/hooks) | Documentation officielle | Intercepter événements, entrées/sorties JSON, codes de sortie et hooks asynchrones. |
| Hooks pratiques | [Claude Code - Automate workflows with hooks](https://code.claude.com/docs/en/hooks-guide) | Documentation officielle | Valider commandes, formater, notifier, imposer règles projet. |
| Skills | [Claude Code - Extend Claude with skills](https://code.claude.com/docs/en/skills) | Documentation officielle | Créer capacités et workflows réutilisables. |
| Permissions | [Claude Code - Configure permissions](https://code.claude.com/docs/en/permissions) | Documentation officielle | Contrôler outils, modes de permission, allow/deny rules. |
| Sandboxing | [Claude Code - Sandboxing](https://code.claude.com/docs/en/sandboxing) | Documentation officielle | Isoler filesystem et réseau pour exécution plus autonome. |
| Sessions | [Claude Code - Work with sessions](https://code.claude.com/docs/en/agent-sdk/sessions) | Documentation officielle | Continuer, reprendre ou forker un run agentique. |
| Instructions projet | [GitHub Copilot - Repository custom instructions](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/add-custom-instructions/add-repository-instructions) | Documentation officielle | Fournir à l'agent les conventions, commandes et validations d'un dépôt. |

## Contexte, mémoire et intégrations

| Domaine | Référence | Nature | Usage dans le processus |
| --- | --- | --- | --- |
| Protocole de contexte | [Model Context Protocol](https://modelcontextprotocol.io/introduction) | Standard ouvert | Connecter agents IA à fichiers, bases, outils, prompts et workflows. |
| Mémoire vectorielle Redis | [Redis - Vector search concepts](https://redis.io/docs/latest/develop/ai/search-and-query/vectors/) | Documentation officielle | Indexer embeddings, filtrer par métadonnées, choisir FLAT/HNSW/SVS-VAMANA. |
| Vector database | [Qdrant Overview](https://qdrant.tech/documentation/overview/) | Documentation officielle | Comprendre collections, points, payloads, HNSW, filtres, sharding et replication. |
| Observabilité | [OpenTelemetry - What is OpenTelemetry?](https://opentelemetry.io/docs/what-is-opentelemetry/) | Documentation officielle | Collecter traces, métriques et logs sans lock-in fournisseur. |
| Kanban et pilotage | [GitHub Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects) | Documentation officielle | Planifier et suivre le travail via projets adaptables et flexibles. |
| CI/CD | [GitHub Actions Documentation](https://docs.github.com/en/actions) | Documentation officielle | Automatiser tests, builds, scans et livraisons. |

## Références logiciel conservées

| Domaine | Référence | Nature | Usage dans le processus |
| --- | --- | --- | --- |
| Exigences | [ISO/IEC/IEEE 29148:2018](https://www.iso.org/standard/72089.html) | Norme internationale | Transformer l'intention client en exigences et critères vérifiables. |
| Architecture | [ISO/IEC/IEEE 42010:2022](https://www.iso.org/standard/74393.html) | Norme internationale | Relier vues d'architecture, parties prenantes et préoccupations. |
| Qualité produit | [ISO/IEC 25010:2023](https://www.iso.org/standard/78176.html) | Norme internationale | Définir les qualités attendues du livrable produit par l'agent. |
| Modélisation logicielle | [OMG UML](https://www.omg.org/spec/UML/) | Spécification OMG | Diagrammes structurels, comportementaux, états, séquences, composants. |
| Processus métier | [OMG BPMN](https://www.omg.org/spec/BPMN/) | Spécification OMG | Processus métier, workflows, responsabilités, événements. |
| Accessibilité | [W3C WCAG 2.2](https://www.w3.org/TR/WCAG22/) | Recommandation W3C | Vérifier les exigences UI produites ou modifiées par l'agent. |
| Contrats API | [OpenAPI Specification](https://spec.openapis.org/oas/latest.html) | Spécification | Décrire et tester les API manipulées par l'agent. |
| Conteneurs | [Docker Docs](https://docs.docker.com/) | Documentation officielle | Standardiser environnements et exécution reproductible. |
| Applications cloud | [The Twelve-Factor App](https://12factor.net/) | Méthodologie de référence | Config, dépendances, logs, build/release/run, parité dev/prod. |
| Performance delivery | [DORA metrics](https://dora.dev/guides/dora-metrics-four-keys/) | Recherche et guide | Mesurer l'impact de l'automatisation sur la livraison. |
| Design discovery | [Design Council Double Diamond](https://www.designcouncil.org.uk/our-resources/the-double-diamond/) | Cadre de référence design | Découverte, définition, développement, livraison. |
| Architecture visuelle | [C4 Model](https://c4model.com/) | Modèle de référence | Diagrammes contexte, containers, composants, code, dynamique, déploiement. |

## Utilisation pratique

- Utiliser ISO/IEC/IEEE 29148 comme colonne vertébrale du besoin client et du cahier des charges.
- Utiliser ISO/IEC/IEEE 42010, C4, UML et BPMN pour choisir les vues qui réduisent réellement le risque.
- Utiliser ISO/IEC 25010 pour transformer la qualité attendue en exigences mesurables.
- Utiliser NIST AI RMF et ISO/IEC 42001 pour gouverner l'usage de l'entreprise-agent et ses risques.
- Utiliser OWASP GenAI et OWASP Top 10 LLM pour sécuriser prompts, outils, données, mémoire et actions autonomes.
- Utiliser les guardrails, evals et red teaming pour traiter les défauts natifs de l'IA : hallucination, surconfiance, prompt injection, mémoire périmée et faux Done.
- Utiliser MCP comme frontière claire entre modèle, outils, données et workflows externes.
- Utiliser Redis ou Qdrant pour le contexte long et chaud seulement avec provenance, métadonnées, politiques d'invalidation et contrôle des données sensibles.
- Utiliser GitHub Projects ou un équivalent Kanban pour rendre le travail visible et éviter l'autonomie opaque.
- Utiliser OpenTelemetry et les traces d'outils pour rendre les runs agentiques auditables, mesurer les SLO, détecter les incidents et améliorer les evals.
