# Parcours d'implémentation agentique

> Statut : annexe informative. Ce document aide à appliquer la norme, mais ne crée pas d'obligation normative. Les obligations sont définies dans [Norme de structure agentique](norme-structure-agentique.md), [Exigences normatives](exigences-normatives-structure-agentique.md) et [Matrice normative maîtresse](matrice-normative-maitresse.md).

Ce parcours transforme le catalogue complet en chemin progressif. Il évite l'anti-pattern consistant à appliquer tous les patterns dès le premier jour.

## Démarrage recommandé

Pour une équipe ou une entreprise qui démarre, commencer par ces huit patterns seulement.

| Ordre | Pattern | Pourquoi maintenant | Preuve minimale |
| --- | --- | --- | --- |
| 1 | ORG-01 Entreprise-agent | Clarifier relation client / agent opérateur. | brief agentique. |
| 2 | ORC-02 Task envelope | Limiter ce que l'agent doit faire. | task envelope rempli. |
| 3 | ORC-03 Handoff packet | Éviter perte d'information entre étapes. | handoff structuré. |
| 4 | GOV-01 Policy engine et hooks | Encadrer les actions risquées. | décision allow/block/escalate. |
| 5 | GOV-07 Tool blast-radius limiter | Limiter fichiers, réseau, environnement et coût. | tool scope / dry-run. |
| 6 | QUA-01 Claim ledger | Ne pas accepter d'affirmation critique sans preuve. | claim sourcé ou hypothèse. |
| 7 | QUA-04 Evidence pack et verification verdict | Fermer une tâche par preuve, pas par confiance. | evidence pack + verdict. |
| 8 | KNO-06 Knowledge Base Indexer | Brancher la documentation de domaine sans la confondre avec mémoire. | knowledge source index. |

## Chemins par profil

| Profil | Objectif | Ajouter ensuite |
| --- | --- | --- |
| Minimal | Structurer missions, lots et preuves. | ORG-02, ORC-01, KNO-01, RUN-02. |
| Contrôlé | Gouverner outils, risques et sources. | GOV-02, GOV-03, GOV-08, GOV-12, KNO-07. |
| Orchestré | Déléguer à plusieurs agents sans dérive. | ORC-04, ORC-05, ORC-09, MOD-01, RUN-06. |
| Gouverné | Mesurer qualité, coût, modèles et incidents. | QUA-08, QUA-09, QUA-10, QUA-13, RUN-08. |
| Production | Exécuter en environnements sensibles. | GOV-10, GOV-11, RUN-03, RUN-10, RUN-11. |

## Règle de lecture

Un pattern est adopté seulement si ses preuves existent. Une documentation sans artefact actif reste une intention d'architecture.

## Exemples prêts à adapter

| Exemple | Usage |
| --- | --- |
| [Workflow feature simple](modeles/exemples/workflow-feature-simple.md) | Décrire un workflow court avec guards et preuves. |
| [Knowledge source repo produit](modeles/exemples/knowledge-source-repo-produit.md) | Greffer une documentation produit versionnée. |
| [LLM provider multi-provider](modeles/exemples/llm-provider-multi-provider.md) | Déclarer Copilot, Claude, Codex, Gemini ou local sans lock-in. |
| [Capability pack reviewer](modeles/exemples/capability-pack-reviewer.md) | Publier une capacité réutilisable avec permissions et tests. |
| [Browser tool validation UI](modeles/exemples/browser-tool-validation-ui.md) | Encadrer une validation navigateur avec DOM, capture et logs. |
