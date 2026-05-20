# Architecture de pilotage agentique

L'architecture de pilotage décrit comment l'entreprise-agent travaille sans réduire le projet à une conversation. Elle sépare les plans de responsabilité : besoin client, contexte, orchestration, outils, qualité, livraison et apprentissage. Le modèle normatif global est défini dans [modele-reference-structure-agentique.md](modele-reference-structure-agentique.md), avec les exigences associées dans [exigences-normatives-structure-agentique.md](exigences-normatives-structure-agentique.md).

## Plans d'architecture

| Plan | Rôle | Artefacts |
| --- | --- | --- |
| Dialogue client | Transformer la demande en besoin testable. | brief, questions ciblées, critères de succès, décisions client |
| Produit et exigences | Conserver la rigueur du processus humain. | CDC niveaux 0 à 3, user stories, acceptation, NFR |
| Orchestration agentique | Décider quel rôle agit, avec quel contexte, quels outils et quelles limites. | prompts, skills, subagents, règles, permissions |
| Runtime agentique | Gouverner les surfaces produites ou modifiées par le système agentique. | agents, skills, hooks, workflows, traces, artefacts, promotion |
| Contexte et mémoire | Rendre le réel accessible sans halluciner ni surcharger la fenêtre de contexte. | workspace, docs, vector DB, Redis chaud, graphe, context pack, journal de preuves |
| Modèles et connaissances | Choisir le bon modèle et gouverner les connaissances indexées ou mémorisées. | routage LLM, fallback, evals modèle, métadonnées, TTL, désindexation, nettoyage |
| Intégrations et outils | Donner des capacités contrôlées à l'agent. | tool registry, MCP, terminal, navigateur, CI, dépôts, API |
| Qualité et sécurité | Bloquer les dérives et prouver le résultat. | hooks, tests, lint, build, scans, evals, red teaming, revues |
| Simulation et reprise | Prévoir l'impact avant action et réparer proprement après incident. | dry-run, checkpoints, rollback, rapport incident, post-mortem |
| Gouvernance d'exécution | Savoir qui agit, avec quel accès, quel coût de contexte et quel validateur. | matrice d'accès, RACI, Kanban enrichi, budget tokens, revues croisées |
| Défauts IA | Rendre visibles et récupérables les erreurs natives du modèle. | registre défauts IA, claim ledger, subagent critique, disconfirmation |
| Livraison et suivi | Rendre le travail visible, acceptable et améliorable. | Kanban, dossier de livraison, monitoring, backlog d'amélioration |

## Position dans le standard

| Document | Rôle |
| --- | --- |
| [terminologie-agentique.md](terminologie-agentique.md) | Définit le vocabulaire stable et le langage normatif. |
| [modele-reference-structure-agentique.md](modele-reference-structure-agentique.md) | Décrit les plans, composants obligatoires et interfaces minimales. |
| [exigences-normatives-structure-agentique.md](exigences-normatives-structure-agentique.md) | Liste les exigences vérifiables par domaine. |
| [patterns/README.md](patterns/README.md) | Classe les patterns réutilisables et anti-patterns par famille. |
| [profils-capacites-agentiques.md](profils-capacites-agentiques.md) | Décrit les capacités minimales par rôle, outil, mémoire et validation. |
| [niveaux-conformite-agentique.md](niveaux-conformite-agentique.md) | Définit les niveaux de maturité et conformité. |
| [runtime-agentique-et-surfaces-gouvernees.md](runtime-agentique-et-surfaces-gouvernees.md) | Décrit la gouvernance des surfaces runtime, hooks, dynamic factory et drift documentaire. |
| [ledger-preuves-verdicts-agentiques.md](ledger-preuves-verdicts-agentiques.md) | Formalise mission ledger, evidence pack et verification verdict. |
| [memoire-hybride-agentique.md](memoire-hybride-agentique.md) | Étend la mémoire vers vectoriel, graphe, sidecar, source registry et memory gate. |
| [matrice-preuves-conformite-agentique.md](matrice-preuves-conformite-agentique.md) | Relie exigences normatives et preuves attendues. |

## Composants principaux

| Composant | Responsabilité | Contrôles clés |
| --- | --- | --- |
| Orchestrateur | Reçoit la mission, découpe, priorise, délègue et synthétise. | plan court, WIP limité, preuves obligatoires |
| Policy engine | Décide ce qui est autorisé selon risque, données, coût et périmètre. | allowlist, denylist, validation humaine, sandbox |
| Runtime surface registry | Inventorie surfaces de contrôle et sorties agentiques. | statut, propriétaire, mode, rétention, preuve |
| Failure mode registry | Liste les défauts IA plausibles pour une mission et les contrôles associés. | hallucination, surconfiance, oubli, faux Done, critique |
| Access control | Applique les rôles, scopes, secrets, tenants et permissions par carte. | RBAC/ABAC, minimisation, journal, validation |
| Validation authority | Définit qui peut accepter, bloquer ou escalader un livrable agentique. | RACI, validateur final, revue croisée, acceptation client |
| Hook engine | Intercepte les moments critiques du cycle agentique. | pre-tool, post-tool, pre-write, pre-release, stop |
| Dynamic factory | Crée agents, workflows, skills, hooks ou instructions quand un gap est détecté. | triage durabilité, validation, usage tracking, promotion/purge |
| Prompt registry | Stocke les instructions stables et contrats de comportement. | versionnement, portée, conflit d'instructions, revue |
| Model router | Choisit le modèle selon rôle, risque, coût, confidentialité et evals. | routage, fallback, benchmark, seuils, logs coût/latence |
| Knowledge janitor | Maintient l'hygiène documentaire et évite que le contexte devienne obsolète. | rétention, archive, désindexation, purge, superseded_by |
| Skills registry | Fournit des procédures réutilisables par domaine. | préconditions, sorties attendues, tests de compétence |
| Tool registry | Liste les outils disponibles et leur niveau de risque. | permission, audit, masquage secrets, quotas |
| MCP gateway | Connecte l'agent à des outils, données et workflows externes via un protocole standard. | serveur autorisé, scopes, logs, timeout, erreurs |
| Orchestrateur de contexte avancé | Arbitre profils, budgets, couches mémoire, exclusions et persistance. | context pack, scorecard, task envelope, handoff packet |
| Token economy | Réduit coût, bruit et saturation par budget, cache, compression et handoff. | budgets, TTL, résumé sourcé, métriques coût/latence |
| Context router | Sélectionne le contexte pertinent avant action. | source, fraîcheur, confiance, taille, priorité |
| Redis chaud | Garde l'état court de session, cache sémantique, file d'événements ou contexte actif. | TTL, invalidation, séparation tenant, données sensibles |
| Base vectorielle | Retrouve connaissances longues par similarité et métadonnées. | embeddings, filtres, top-k, score, provenance, réindexation |
| Journal de preuves | Trace ce qui a été lu, décidé, exécuté et vérifié. | horodatage, source, résultat, limite, décision |
| Mission ledger | Journal append-only des missions, tâches, transitions et incidents. | événements, machine d'état, audit, non-répudiation |
| Claim ledger | Relie chaque affirmation importante à une preuve ou la marque comme hypothèse. | source, résultat d'outil, confiance, limite |
| Evidence pack | Regroupe preuves atomiques et couverture de critères. | digest, profils de preuve, verdict, décision |
| Kanban | Rend visibles lots, états, blocages et acceptation. | DoR, DoD, WIP, dépendances, priorité, risque |
| Subagents | Isolent des travaux spécialisés ou volumineux. | outil limité, prompt spécialisé, résumé, revue croisée |
| Observabilité | Rend compréhensible le comportement du système agentique. | traces, métriques, logs, coût, latence, taux d'échec |
| Eval harness | Teste prompts, modèles, subagents et workflows sur cas représentatifs. | jeux de cas, scorecard, seuils, régression |
| Incident response | Détecte, contient, répare et capitalise les erreurs agentiques. | rollback, purge mémoire, post-mortem, backlog prévention |

## Contexte : chaud, froid et sourcé

| Type de contexte | Stockage possible | Usage | Risque à maîtriser |
| --- | --- | --- | --- |
| Contexte immédiat | Fenêtre de conversation, notes de mission | Objectif, décisions récentes, plan en cours | saturation, oubli après compaction |
| Contexte chaud | Redis, cache session, état de workflow | tâches en cours, résultats temporaires, cache sémantique | fuite de données, contexte périmé, mélange de missions |
| Contexte long terme | Base vectorielle, mémoire projet, docs indexées | RAG, similarité, patterns, décisions historiques | rappel approximatif, source faible, embeddings obsolètes |
| Contexte de vérité | Workspace, tests, CI, dépôts, docs officielles | Preuve actuelle du produit | lecture incomplète, fichiers générés non fiables |
| Contexte externe | Web, API, MCP, tickets, Kanban | Références, état projet, exigences externes | réseau, prompt injection, données non vérifiées |

Le contexte doit être sélectionné avant l'action, mais aussi critiqué. Un résultat de base vectorielle ou de cache chaud n'est pas une vérité : il devient exploitable seulement s'il conserve une provenance, un score, une date et un lien avec le besoin.

## Context orchestration layer

Cette couche pilote la taille du contexte comme un budget. Elle évite de saturer l'orchestrateur principal tout en donnant aux subagents juste ce qu'il faut pour réussir leur étape. Le détail complet est disponible dans [orchestration-contexte-agentique.md](orchestration-contexte-agentique.md).

| Décision | Question | Sortie |
| --- | --- | --- |
| Étape courante | Sommes-nous en intake, cadrage, architecture, implémentation, QA, sécurité, livraison ou capitalisation ? | stage actif |
| Profil de contexte | Quel rôle doit travailler et de quoi a-t-il besoin ? | profil intake, discovery, architecture, dev, QA, sécurité, livraison |
| Budget de contexte | Quelle quantité maximale est utile ? | tiny, small, medium, deep |
| Plan de récupération | Où chercher et avec quels seuils ? | Redis, vector DB, workspace, docs, CI, Kanban |
| Critique du contexte | Les sources sont-elles fraîches, fiables et non sensibles ? | contexte validé ou question/escalade |
| Délégation | Quel contrat donner au subagent ? | task envelope |
| Passage de relais | Que garder pour la suite ? | handoff packet |
| Persistance | Que stocker, invalider ou oublier ? | Redis, vector DB, Kanban, journal, docs |

## Profils et budgets de contexte

| Étape | Budget recommandé | Contexte minimal |
| --- | --- | --- |
| Intake | small | demande client, objectifs, contraintes connues, état Kanban |
| Discovery | medium | sources projet, mémoire vectorielle filtrée, hypothèses, questions |
| Architecture | deep | CDC, contraintes qualité, existant, ADR, références, risques |
| Implémentation | small | carte, fichiers ciblés, conventions locales, tests liés |
| QA | small | diff, critères d'acceptation, commandes de validation |
| Sécurité | medium | périmètre, données, outils, menaces, dépendances |
| Livraison | small | preuves, changelog, risques résiduels, décisions client |
| Capitalisation | tiny | décision validée, apprentissage stable, source, portée |

Le budget peut être augmenté quand un hook signale un contexte insuffisant, mais il doit être réduit après synthèse. L'objectif est de déplacer des paquets courts et sourcés, pas de déplacer toute la conversation.

## Contrats de délégation

| Contrat | Contenu | Pourquoi |
| --- | --- | --- |
| Task envelope | mission, étape, rôle, budget, contexte minimal, outils, critères, sortie attendue | éviter qu'un subagent cherche ou modifie hors périmètre |
| Handoff packet | résultat, preuves, hypothèses, risques, changements, mémoire, prochain trigger | déclencher la suite sans recharger tout l'historique |
| Memory write request | fait stable, source, portée, sensibilité, durée de vie | éviter la mémoire polluée ou dangereuse |
| Stage transition request | DoD étape, preuves, blocages, décision attendue | empêcher un passage prématuré |

## Prompts, instructions et skills

Les prompts de base par rôle sont fournis dans [prompts-subagents-agentiques.md](prompts-subagents-agentiques.md). Ils doivent rester stables : le contexte variable appartient au task envelope.

| Élément | Usage | Bonne pratique |
| --- | --- | --- |
| Instructions globales | Définissent le comportement stable de l'agent. | Courtes, non contradictoires, orientées qualité. |
| Instructions projet | Décrivent conventions, build, tests, structure et préférences locales. | Versionnées, vérifiées, mises à jour après apprentissage. |
| Prompts de mission | Traduisent le besoin client en tâche exécutable. | Inclure objectif, contexte, contraintes, preuves attendues. |
| Skills | Encapsulent une méthode réutilisable : audit, cadrage, test, rédaction, sécurité. | Définir quand les invoquer et quel livrable produire. |
| Prompt d'évaluation | Vérifie une sortie agentique sur cas représentatifs. | Séparer génération et jugement, conserver les exemples. |

## Gouvernance d'exécution

La matrice détaillée de Kanban, accès, validation, économie de tokens, communication inter-agents et conformité de contexte est disponible dans [gouvernance-execution-agentique.md](gouvernance-execution-agentique.md).

| Sujet | Règle courte |
| --- | --- |
| Kanban | Chaque carte porte owner, validateur, contexte, budget, accès, preuves et handoff. |
| Accès | Accorder la capacité minimale nécessaire au lot, jamais un accès général par confiance. |
| Validation | Le client valide métier et acceptation ; QA, sécurité, ops et design valident leurs domaines. |
| Tokens | Commencer petit, récupérer ciblé, compresser avant délégation, mesurer coût et rework. |
| Communication agents | Autorisée par consultation tracée ou atelier court, sous contrôle de l'orchestrateur. |
| Conformité contexte | Chaque rôle a ses sources obligatoires, par exemple charte graphique pour UI/DA. |

## Défauts IA et contre-mesures

La couche complète est décrite dans [defauts-ia-et-fiabilite.md](defauts-ia-et-fiabilite.md). Elle ajoute une logique de défi systématique : l'agent doit prouver, calibrer et chercher ce qui pourrait contredire sa conclusion.

| Défaut | Contrôle architectural |
| --- | --- |
| Hallucination | claim ledger, source obligatoire, vérification outil. |
| Surconfiance | barrière de calibration, critique indépendante, limites explicites. |
| Complaisance | questions de disconfirmation, rôle critique, validation client. |
| Oubli de contexte | task envelope, handoff packet, décisions actives. |
| Faux Done | pre-done hook, QA indépendante, preuve de commande. |
| Mémoire polluée | pre-memory-write, TTL, source originale, invalidation. |
| Écho multi-agents | critique/red-team, sources distinctes, revue croisée. |

## Observabilité, evals et SLO

Le modèle complet de mesure est décrit dans [observabilite-evals-slo-agentiques.md](observabilite-evals-slo-agentiques.md). Les SLO agentiques suivent non seulement le délai et la qualité, mais aussi les faux Done, hallucinations détectées, coûts tokens, escalades de contexte et validations humaines.

## Simulation, incidents et reprise

Les actions risquées doivent passer par [simulation-pre-execution-agentique.md](simulation-pre-execution-agentique.md). Quand une erreur survient, le processus de [incidents-et-reprise-agentique.md](incidents-et-reprise-agentique.md) définit détection, containment, rollback, purge mémoire, correction et post-mortem.

## Modèles, connaissances et contrats

La gouvernance des modèles et connaissances est décrite dans [gouvernance-modeles-et-connaissances.md](gouvernance-modeles-et-connaissances.md), et le flux détaillé de routage LLM/rétention dans [routage-llm-retention-connaissances.md](routage-llm-retention-connaissances.md). Les contrats d'interface et templates prêts à remplir sont rassemblés dans [contrats-operationnels-agentiques.md](contrats-operationnels-agentiques.md).

## Outils et MCP

Les outils sont classés par niveau d'impact.

| Niveau | Exemples | Politique recommandée |
| --- | --- | --- |
| Lecture locale | recherche fichiers, lecture docs, diagnostics éditeur | autorisé par défaut dans le workspace |
| Vérification locale | tests, lint, build, rendu Mermaid, smoke local | autorisé si coût raisonnable et pas de donnée externe |
| Écriture locale | édition fichiers, génération docs, formatage | autorisé dans le périmètre validé, avec diff |
| Réseau contrôlé | web docs, API de lecture, téléchargement dépendance | autorisation ou politique explicite selon sensibilité |
| Système externe | GitHub, cloud, tickets, bases de données, navigateur | MCP ou outil identifié, scopes limités, journal obligatoire |
| Production ou secrets | déploiement, rotation, migration, données personnelles | validation humaine explicite et procédure dédiée |

MCP sert de passerelle standardisée entre l'agent et les systèmes externes. Il doit être traité comme une surface d'intégration : chaque serveur MCP doit avoir un propriétaire, un périmètre, des scopes, une stratégie d'erreur, des logs et une règle d'arrêt.

## Hooks de contrôle

| Hook | Moment | Objectif | Exemple de blocage |
| --- | --- | --- | --- |
| Pre-action | Avant plan ou délégation risquée | Vérifier périmètre, mission, données, coût. | besoin non testable, règles sécurité absentes |
| Pre-context-load | Avant récupération de contexte | Vérifier budget, sources autorisées, sensibilité. | contexte demandé trop large, source interdite |
| Pre-context-reuse | Avant réutilisation d'une source | Vérifier statut, fraîcheur, remplacement et rétention. | source obsolète, expirée ou superseded |
| Post-context-load | Après récupération de contexte | Critiquer score, fraîcheur, contradictions et volume. | mémoire périmée, documents contradictoires |
| Pre-delegation | Avant lancement subagent | Vérifier task envelope, outils, sortie attendue. | subagent trop autonome, contexte insuffisant |
| Pre-model-call | Avant appel modèle | Vérifier modèle, confidentialité, coût et budget. | modèle non autorisé, données sensibles |
| Pre-model-route | Avant choix modèle | Qualifier tâche, risque, modalité et fallback. | routage implicite ou modèle non évalué |
| Pre-tool | Avant appel d'outil | Autoriser ou refuser selon outil et paramètres. | commande destructive, accès secret, requête réseau non prévue |
| Post-tool | Après appel d'outil | Capturer résultat, erreur, preuve ou anomalie. | test échoué, sortie trop volumineuse, donnée sensible affichée |
| Pre-write | Avant écriture fichier ou modification externe | Vérifier diff attendu et ownership. | fichier hors périmètre, config sécurité, migration non validée |
| Pre-memory-write | Avant écriture Redis, vector DB ou mémoire | Vérifier source, portée, TTL et absence de secret. | fait non validé, donnée sensible |
| Pre-index | Avant indexation vectorielle | Vérifier durabilité, sensibilité, owner et métadonnées. | rapport temporaire, source sensible, TTL absent |
| Scheduled-cleanup | Périodique | Archiver, désindexer ou purger les artefacts périmés. | documents obsolètes, embeddings anciens |
| Doc-drift-check | Après changement de surface runtime | Détecter divergence docs, manifests, hooks, workflows et mémoire. | doc annonce un comportement absent |
| Hook-promotion | Avant passage shadow/canary/enforced | Vérifier faux positifs, couverture et risque. | hook nouveau trop bloquant |
| Pre-stage-transition | Avant passage d'étape | Vérifier DoD, handoff packet et prochain trigger. | preuves absentes, décision client nécessaire |
| Pre-dry-run | Avant action risquée | Exiger plan, impact, permissions, rollback. | action externe ou irréversible non simulée |
| Incident-detected | Dès anomalie critique | Stopper, contenir, diagnostiquer et escalader. | faux Done, fuite, action non autorisée |
| Pre-release | Avant livraison ou PR | Exiger DoD, tests, scans, dossier d'acceptation. | build absent, risque critique ouvert, review manquante |
| Stop | Fin de tâche ou arrêt subagent | Résumer, tracer, nettoyer, mettre à jour mémoire si validée. | mémoire non sourcée, livrable sans preuve |

## Subagents

| Subagent | Mission | Outils typiques | Sortie attendue |
| --- | --- | --- | --- |
| Analyste besoin | Clarifier problème, valeur, utilisateurs, critères. | lecture, recherche, questions | note de cadrage, hypothèses, questions ouvertes |
| Architecte | Choisir vues, frontières, ADR, risques. | lecture, diagrammes, références | option recommandée, compromis, ADR |
| Design UI/UX et DA | Garantir parcours, accessibilité, design system, charte graphique et intention visuelle. | maquettes, captures, design system, références | recommandations UX/UI, règles DA, critères visuels |
| Développeur | Implémenter un lot ciblé. | édition, tests, terminal | patch, tests, notes de changement |
| QA | Définir et exécuter validations. | tests, navigateur, rendu, diagnostics | rapport de vérification, défauts |
| Sécurité | Examiner menaces, secrets, dépendances, prompt injection. | lecture, scans, règles | risques, sévérité, corrections |
| Critique et red team | Chercher hallucinations, surconfiance, faux Done, contradictions et preuves faibles. | lecture, claim ledger, evals, revue | objections, risques, preuves manquantes, go/no-go |
| Ops | Vérifier build, CI/CD, déploiement, observabilité. | terminal, CI, logs, cloud si autorisé | runbook, checklist, alertes |
| Documentation | Mettre à jour docs, modèles, références. | édition, rendu, liens | documentation cohérente et vérifiée |

Les subagents doivent être spécialisés et limités. Un subagent de recherche peut être lecture seule. Un subagent de QA peut exécuter des tests mais ne pas écrire. Un subagent de sécurité peut bloquer une livraison sans modifier le produit.

## Kanban agentique

| Colonne | Critère d'entrée | Critère de sortie |
| --- | --- | --- |
| Idées / signaux | Demande, incident, opportunité, dette. | mission qualifiée ou rejetée |
| Cadrage | Besoin encore incomplet. | CDC niveau 0 validé |
| Prêt | User story, critères, contexte et preuves attendues. | lot sélectionné par l'orchestrateur |
| En cours | Subagent ou agent principal assigné. | changement produit ou rapport prêt à vérifier |
| Vérification | Tests, scans, rendu, review ou evals en cours. | qualité prouvée ou retour en correction |
| Validation client | Décision humaine attendue. | accepté, ajusté ou refusé |
| Livré / capitalisé | Livrable accepté. | mémoire, docs, backlog et suivi mis à jour |

## Observabilité et fiabilité

| Signal | Utilité |
| --- | --- |
| Traces | Comprendre le chemin : prompt, contexte, outils, subagents, décisions. |
| Métriques | Suivre coût, latence, taux d'échec, rework, validations bloquées. |
| Logs | Diagnostiquer erreurs d'outil, permissions, hooks, accès externes. |
| Evals | Mesurer la qualité de réponses et décisions agentiques sur cas représentatifs. |
| Red teaming | Tester prompt injection, exfiltration, actions excessives et contournements. |
| Revues humaines | Valider produit, architecture, sécurité complexe et acceptation finale. |

## Boucle d'amélioration

1. Capturer le besoin et les décisions client.
2. Transformer le besoin en CDC et backlog.
3. Exécuter par lots orchestrés.
4. Vérifier avec preuves et hooks.
5. Livrer avec dossier d'acceptation.
6. Mesurer incidents, rework, coûts, satisfaction et qualité.
7. Mettre à jour instructions, skills, mémoire, tests, evals et backlog.
