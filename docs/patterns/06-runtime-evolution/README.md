# Patterns runtime et évolution

Ces patterns gouvernent les capacités et sorties produites par le runtime agentique afin d'éviter la prolifération invisible.

La source Mermaid de cette famille est disponible dans [../../../diagrammes/patterns-runtime-evolution.mmd](../../../diagrammes/patterns-runtime-evolution.mmd).

## RUN-01 : Dynamic factory contrôlée

| Élément | Description |
| --- | --- |
| Intention | Créer de nouvelles capacités sans prolifération incontrôlée. |
| Problème | Agents, skills et workflows dynamiques peuvent devenir une dette invisible. |
| Solution | Détecter le gap, classer l'artefact, décider éphémère/permanent, valider puis promouvoir ou purger. |
| Contrôles | Usage tracking, expiration, score de durabilité, review, registre. |
| Anti-pattern | Créer un agent permanent pour chaque demande ponctuelle. |

## RUN-02 : Runtime output governance

| Élément | Description |
| --- | --- |
| Intention | Gouverner les artefacts produits par le runtime agentique. |
| Problème | Plans, traces, rapports, captures et sorties temporaires s'accumulent sans statut. |
| Solution | Déclarer type, propriétaire, sensibilité, rétention, indexation et statut. |
| Contrôles | Registre de surfaces runtime, cleanup, doc drift, audit périodique. |
| Anti-pattern | Laisser les sorties runtime devenir une documentation parallèle non fiable. |

## RUN-03 : Kubernetes agent control plane

| Élément | Description |
| --- | --- |
| Intention | Exécuter agents et sandboxes en production comme ressources réconciliées, isolées et observables. |
| Problème | Un worker local ne suffit pas pour quotas, scheduling, multi-tenant, service accounts et tolérance de panne. |
| Solution | Fournir un provider K8s natif : pods gérés directement, requests/limits, node selectors, tolerations, affinity, service accounts, images prebaked et télémétrie OTel. |
| Contrôles | Admission policy, network allowlist, quotas, image provenance, service account minimal, SLO runtime. |
| Anti-pattern | Lancer des agents en cluster via scripts ad hoc sans contrat de ressources ni observabilité. |

## RUN-04 : Orders exec/formula dispatcher

| Élément | Description |
| --- | --- |
| Intention | Choisir le coût et le niveau d'orchestration appropriés pour un ordre. |
| Problème | Toutes les commandes ne nécessitent pas une session agent ; inversement certains workflows shell cachent une orchestration complexe. |
| Solution | Distinguer `exec` (shell-only, sans session agent) et `formula` (workflow agentique instancié), avec budget, preuve et blast-radius différents. |
| Contrôles | Type d'ordre, budget token, policy tool, evidence attendu, classification risque. |
| Anti-pattern | Lancer un agent complet pour une commande déterministe ou exécuter un workflow risqué comme simple shell. |

## RUN-05 : Primitive-first capability model

| Élément | Description |
| --- | --- |
| Intention | Éviter que les rôles et capacités deviennent des types SDK rigides. |
| Problème | Un framework role-centric pousse à forker le core dès qu'un rôle ou workflow change. |
| Solution | Définir rôles, prompts, formules et permissions dans des packs/configs ; le SDK ne fournit que les primitives d'exécution et de composition. |
| Contrôles | Registry de packs, résolution de conflits, tests de compétence, versioning et promotion. |
| Anti-pattern | Encoder Mayor/Reviewer/Builder comme classes SDK non composables. |

## RUN-06 : Capability marketplace

| Élément | Description |
| --- | --- |
| Intention | Rendre les capacités agentiques découvrables, gouvernées et réutilisables. |
| Problème | Agents, prompts, skills, outils et workflows se multiplient sans catalogue ni statut. |
| Solution | Publier des capability packs avec owner, version, runtime compatible, permissions, tests et lifecycle. |
| Contrôles | Capability pack manifest, skill record, tests de compétence, usage telemetry, retirement. |
| Anti-pattern | Copier-coller des prompts et scripts d'équipe en équipe sans source d'autorité. |

## RUN-07 : Skill/capability lifecycle

| Élément | Description |
| --- | --- |
| Intention | Promouvoir ou retirer les skills selon preuve d'utilité et de sécurité. |
| Problème | Une skill expérimentale peut devenir critique sans review, ou une skill obsolète rester active. |
| Solution | Utiliser les statuts draft, experimental, canary, enforced, deprecated, retired avec gates et owner. |
| Contrôles | Skill record, eval, telemetry usage, false positive review, changelog. |
| Anti-pattern | Installer une skill comme permanente parce qu'elle a aidé une fois. |

## RUN-08 : Runtime provider contract

| Élément | Description |
| --- | --- |
| Intention | Séparer l'orchestration logique du backend d'exécution réel. |
| Problème | Le même workflow doit pouvoir tourner localement, dans un IDE, sur worker distant ou cluster sans changer ses garanties. |
| Solution | Normaliser lifecycle, ressources, logs, health, secrets, cleanup et policies via un runtime provider contract. |
| Contrôles | Runtime provider contract, provider health, env scrub, quotas, workspace isolation. |
| Anti-pattern | Écrire des workflows dépendants d'un shell local non déclaré. |

## RUN-09 : Agent backend boundary

| Élément | Description |
| --- | --- |
| Intention | Isoler le backend agent des modèles, outils et environnements spécifiques. |
| Problème | Un agent couplé à un fournisseur ou runtime ne peut pas migrer entre Copilot, Codex, Claude, local ou cluster. |
| Solution | Définir des ports : model provider, tool provider, memory provider, runtime provider et telemetry provider. |
| Contrôles | Provider registry, adapter contract, fallback explicite, eval de compatibilité. |
| Anti-pattern | Appeler directement un SDK provider dans la logique métier du workflow. |

## RUN-10 : Local agent worker pool

| Élément | Description |
| --- | --- |
| Intention | Exécuter plusieurs tâches locales sans bloquer l'orchestrateur. |
| Problème | Les missions longues, tests ou explorations concurrentes saturent une seule session et masquent les pannes. |
| Solution | Gérer un pool de workers locaux avec capacité, queue, timeout, health, logs et cleanup. |
| Contrôles | WIP limit, runtime provider contract, telemetry, workspace isolation, cancellation. |
| Anti-pattern | Lancer des agents locaux en arrière-plan sans registre ni arrêt fiable. |

## RUN-11 : Workspace isolation

| Élément | Description |
| --- | --- |
| Intention | Empêcher les agents de modifier ou lire hors du périmètre autorisé. |
| Problème | Un agent outillé peut toucher fichiers, secrets, caches ou repos voisins par accident. |
| Solution | Déclarer workspace root, mounts, write zones, secrets visibles, network policy et cleanup. |
| Contrôles | Path allowlist, sandbox, secret scan, runtime provider, blast-radius. |
| Anti-pattern | Laisser l'agent opérer depuis un répertoire parent contenant plusieurs projets. |

## RUN-12 : Secure local coordinator

| Élément | Description |
| --- | --- |
| Intention | Coordonner plusieurs agents locaux sans proxy de credentials ni canal opaque. |
| Problème | Un coordinateur local peut devenir un relais de tokens, un bus non audité ou un contournement des policies. |
| Solution | Utiliser inbox signée, terminal bridge officiel, sessions bornées, env scrub et gates avant action. |
| Contrôles | Agent privilege boundary, runtime provider contract, trajectory logging, policy engine. |
| Anti-pattern | Faire transiter les tokens Copilot/Claude/Codex d'un outil vers un autre via un proxy maison. |

## Interfaces liées

| Interface | Rôle |
| --- | --- |
| Registre des surfaces runtime | Inventorie agents, skills, hooks, workflows, traces et artefacts. |
| Registre des capacités dynamiques | Suit promotion, expiration, propriétaire et preuves. |
| Politique de rétention | Détermine ce qui devient durable, archive, TTL ou purge. |
| Runtime provider contract | Définit lifecycle, ressources, logs, exec et health pour un backend local ou K8s. |
| Order dispatcher contract | Normalise `exec` vs `formula`, budget, risque et preuves attendues. |
| Capability pack manifest | Déclare rôle, prompts, permissions, imports, tests et compatibilité runtime. |
| Skill record | Décrit activation, permissions, limites et preuves d'une skill. |
| Workspace policy | Déclare root, mounts, secrets, write zones et cleanup. |
| Secure local coordination contract | Déclare canaux, signatures, sessions, secrets et gates. |
