# Gouvernance d'exécution agentique

Cette page transforme le processus agentique en règles opérables : Kanban, sécurité, accès, validation, économie de tokens, prompts, communication entre agents et conformité au contexte métier ou créatif.

## Réponse courte aux questions de pilotage

| Question | Réponse actuelle du process | Complément opérationnel |
| --- | --- | --- |
| Le Kanban est-il à jour avec le process ? | Oui pour les colonnes, DoR, DoD, WIP et blocages. | Ajouter des champs obligatoires par carte : contexte, accès, validateur, budget de tokens, subagents, preuves et handoff. |
| La sécurité et les accès sont-ils couverts ? | Oui via policy engine, hooks, permissions, sandbox, MCP et points de validation. | Formaliser une matrice RBAC/ABAC par outil, source, donnée et environnement. |
| Qui valide le travail des agents ? | Le client valide le métier et l'acceptation finale ; QA, sécurité et ops valident leurs domaines. | Mettre une chaîne de validation explicite par type de carte et niveau de risque. |
| Existe-t-il une économie de tokens ? | Oui via budgets de contexte et task envelopes. | Ajouter des règles de compression, cache, réutilisation, escalade, routage LLM et mesure de coût. |
| Les modèles IA sont-ils gouvernés ? | Pas assez si le modèle est implicite. | Ajouter routage par tâche/rôle, fallback, evals, confidentialité et coût. |
| Les connaissances obsolètes sont-elles nettoyées ? | Oui si une politique de rétention est appliquée. | Ajouter source active, TTL, superseded_by, désindexation, purge et knowledge janitor. |
| Les prompts sont-ils générés pour chaque agent ? | Le prompt registry est prévu. | Ajouter des prompts de base versionnables pour chaque rôle. |
| Les agents doivent-ils communiquer entre eux ? | Oui, mais pas librement par défaut. | Les échanges passent par l'orchestrateur, ou par une consultation pair-à-pair tracée avec question, contexte, réponse et impact. |
| Chaque agent utilise-t-il le contexte dont il a besoin ? | Oui via profils de contexte. | Ajouter une checklist de conformité par rôle : design, DA, UX, dev, QA, sécurité, ops, documentation. |
| Les défauts IA sont-ils pris en compte ? | Partiellement via garde-fous, preuves et evals. | Ajouter registre défauts IA, claim ledger, critique/red-team et hooks anti-surconfiance. |
| Que se passe-t-il en cas d'erreur ? | Les garde-fous bloquent une partie des risques. | Ajouter incident response, rollback, purge mémoire et post-mortem. |

## Kanban agentique mis à jour

Le Kanban ne doit pas seulement suivre l'état du travail. Il doit aussi porter les décisions qui rendent l'autonomie contrôlable.

| Colonne | Critère d'entrée | Critère de sortie | Champs obligatoires |
| --- | --- | --- | --- |
| Signal | Demande, idée, incident, dette ou risque. | Mission qualifiée ou rejetée. | demandeur, valeur supposée, type de mission |
| Cadrage | Besoin incomplet ou risque non qualifié. | CDC niveau 0 validé. | validateur métier, scope, hors-scope, risques |
| Prêt | User story ou lot testable. | Lot sélectionné par l'orchestrateur. | DoR, critères d'acceptation, sources, accès, budget contexte |
| En cours | Agent ou subagent assigné. | Changement, analyse ou livrable prêt à vérifier. | owner agentique, task envelope, WIP, journal |
| Consultation | Besoin d'un avis spécialisé. | Réponse intégrée ou décision escaladée. | agent demandeur, agent consulté, question, contexte partagé |
| Vérification | Preuves en cours. | Qualité prouvée ou retour correction. | tests, scans, rendu, review, evals, logs |
| Sécurité / conformité | Risque sécurité, donnée, accès ou prompt injection à examiner. | Risque accepté, corrigé ou bloquant. | menace, sévérité, contrôle, approbation |
| Validation client | Décision humaine attendue. | Accepté, ajusté ou refusé. | dossier d'acceptation, risques résiduels, décision |
| Livré | Livrable accepté. | Capitalisation effectuée. | changelog, handoff final, mémoire, backlog suite |
| Capitalisé | Apprentissage à conserver. | Mémoire/docs/evals mis à jour ou oubli décidé. | fait stable, source, portée, TTL, sensibilité, rétention |

## Champs de carte obligatoires

| Champ | Pourquoi |
| --- | --- |
| Type de mission | Détermine le niveau de cadrage, de sécurité et de validation. |
| Niveau de risque | Pilote hooks, revues, accès et validation humaine. |
| Validateur final | Évite qu'un agent s'auto-accepte sur un sujet métier. |
| Sources de vérité | Empêche la décision basée sur mémoire approximative. |
| Défauts IA plausibles | Force à anticiper hallucination, oubli, complaisance, faux Done ou dérive. |
| Claim ledger | Relie les affirmations clés aux sources ou résultats d'outils. |
| Profil de contexte | Assure que le bon rôle reçoit le bon contexte. |
| Budget de contexte | Limite coût, bruit et pollution de la fenêtre. |
| Routage LLM | Rend explicite modèle, fallback, evals, coût et confidentialité. |
| Task envelope | Cadre mission, outils, périmètre et sortie attendue. |
| Handoff packet | Permet à l'étape suivante de repartir d'une preuve courte. |
| Permissions outils | Sépare lecture, écriture, réseau, MCP, dépôt distant et production. |
| Modèle IA et fallback | Rend visible coût, confidentialité et capacité de raisonnement. |
| Rétention et nettoyage | Décide mémoire durable, archive, désindexation ou purge. |
| Dry-run | Simule l'impact avant action risquée. |
| Subagents impliqués | Rend visible qui a produit quoi. |
| Preuves attendues | Rend le Done vérifiable. |
| Décisions ouvertes | Évite de cacher une incertitude métier ou sécurité. |

## Sécurité, accès et permissions

Les accès sont accordés par capacité, pas par confiance générale dans l'agent. Une carte ne donne accès qu'aux outils nécessaires au livrable.

| Niveau d'accès | Autorisation par défaut | Exemples | Validation requise |
| --- | --- | --- | --- |
| Lecture locale | Oui dans le workspace. | rechercher, lire fichiers, diagnostics. | non, sauf dossier sensible. |
| Vérification locale | Oui si coût raisonnable. | tests, lint, build, rendu. | non, sauf environnement lourd ou payant. |
| Écriture locale | Oui dans le scope validé. | modifier docs, code ciblé, config non sensible. | revue diff ou hook pre-write. |
| Réseau lecture | Non par défaut si données projet exposées. | docs officielles, API lecture, téléchargement. | politique source ou accord. |
| MCP externe | Non par défaut. | GitHub, Figma, Kanban, DB, cloud. | serveur autorisé, scopes, logs. |
| Dépôt distant | Non par défaut. | push, PR, commentaire, release. | accord explicite ou règle projet. |
| Données sensibles | Non par défaut. | secrets, PII, credentials, production data. | procédure dédiée, minimisation. |
| Production | Non par défaut. | déploiement, migration, suppression. | validation humaine explicite. |

## Matrice de validation

| Livrable ou décision | Validateur principal | Validateurs de soutien | Blocage si absent |
| --- | --- | --- | --- |
| Besoin, valeur, priorités | Client utilisateur | analyste besoin | oui |
| Charte graphique, DA, ton, marque | Client ou direction artistique | designer, UX, documentation | oui si interface ou contenu public |
| Architecture structurante | Architecte humain ou client technique | sécurité, ops, dev | oui si impact durable |
| Code ou patch local | QA agentique ou revue pair | dev, CI | oui si tests absents sans justification |
| UX ou UI | UX/UI designer ou client produit | accessibilité, QA visuelle | oui si charte ou parcours absent |
| Sécurité et accès | Responsable sécurité ou client autorisé | sécurité agentique, ops | oui si risque moyen ou plus |
| Dépendance ou outil externe | Client technique ou ops | sécurité, dev | oui si lock-in, coût ou supply chain |
| Action MCP externe | Propriétaire du système | ops, sécurité | oui si écriture ou donnée sensible |
| Livraison finale | Client utilisateur | QA, sécurité, ops, documentation | oui |
| Mémoire persistante | Orchestrateur | sécurité, propriétaire contexte | oui si source ou portée absente |
| Rétention ou purge de connaissance | Knowledge janitor ou orchestrateur | propriétaire de la source | oui si source active ou sensible |
| Fermeture d'une carte à risque | Critique ou QA | sécurité, design, ops selon domaine | oui si claim ledger ou preuve absent |

Un agent peut recommander, vérifier et bloquer. Il ne doit pas être le seul validateur d'une décision métier, d'un accès sensible, d'une architecture durable ou d'une acceptation finale.

## Économie de tokens et de contexte

L'économie de tokens est une discipline de conception. Elle ne cherche pas seulement à réduire le coût : elle réduit aussi la confusion, les hallucinations et les oublis.

| Mécanisme | Règle |
| --- | --- |
| Budget par étape | `tiny`, `small`, `medium` ou `deep` avant toute délégation. |
| Compression avant délégation | Remplacer l'historique par sources, contraintes, décisions et critères. |
| Cache chaud Redis | Stocker l'état court avec TTL, pas les secrets ni les gros logs. |
| Recherche vectorielle filtrée | Récupérer par métadonnées avant similarité large. |
| Rétention documentaire | Ne pas indexer les brouillons, handoffs temporaires ou sources expirées. |
| Résumé de gros document | Résumer avec provenance et date, puis relire la source si décision critique. |
| Escalade contrôlée | Augmenter le budget seulement après preuve d'insuffisance. |
| Handoff obligatoire | Ne pas transmettre tout le contexte : transmettre résultat, preuves, risques et trigger. |
| Mesure | Suivre tokens, coût, latence, rework, taux de contexte inutile et escalades. |

### Règle d'escalade

1. Commencer avec le plus petit budget compatible avec le rôle.
2. Si le subagent signale une contrainte manquante, récupérer une source de vérité ciblée.
3. Si deux sources se contredisent, escalader à l'orchestrateur ou au client.
4. Si le budget `deep` est nécessaire, produire une synthèse `small` avant passage d'étape.

## Défauts IA dans le Kanban

La gestion détaillée des modes d'échec est décrite dans [defauts-ia-et-fiabilite.md](defauts-ia-et-fiabilite.md). En pratique, toute carte non triviale doit ajouter une ligne courte : “qu'est-ce que l'IA risque de rater ici ?”.

| Défaut plausible | Contrôle sur la carte |
| --- | --- |
| Hallucination de fait | source officielle, fichier lu ou résultat d'outil. |
| Surconfiance | hypothèses séparées des faits, critique si risque moyen. |
| Complaisance | question de disconfirmation avant décision. |
| Oubli de contrainte | handoff et décisions actives attachés à la carte. |
| Faux Done | QA ou pre-done hook avec preuve de fermeture. |
| Écho multi-agents | critique indépendante ou source distincte. |

## SLO, modèles et incidents dans le Kanban

| Élément | À renseigner sur la carte |
| --- | --- |
| SLO | délai attendu, coût maximal, preuve de fermeture, niveau de qualité. |
| Modèle | modèle choisi par tâche, raison, fallback, contrainte confidentialité. |
| Evals | cas à exécuter ou seuil attendu. |
| Rétention | artefacts durables, temporaires, à archiver, désindexer ou purger. |
| Dry-run | requis ou non, validation attendue, rollback. |
| Incident | procédure applicable, propriétaire, surface à purger si erreur. |

## Prompts par agent

Chaque agent doit avoir un prompt stable, versionné et limité. Le prompt ne contient pas tout le contexte de mission : il décrit le rôle, les limites, le format de sortie et les critères de preuve. Le contexte réel arrive par task envelope.

Les prompts de base sont disponibles dans [prompts-subagents-agentiques.md](prompts-subagents-agentiques.md).

## Communication entre agents

Les agents peuvent communiquer, mais la communication doit être intentionnelle. Par défaut, ils ne discutent pas librement : ils échangent des paquets courts pour éviter bruit, dérive et perte de responsabilité.

| Cas | Mode recommandé | Exemple |
| --- | --- | --- |
| Question simple entre rôles | Consultation tracée via orchestrateur. | Le dev demande au designer quel composant respecte la charte. |
| Décision avec impact transversal | Atelier agentique court. | Architecte, sécurité et ops comparent deux options. |
| Vérification indépendante | Revue croisée. | QA vérifie le patch dev ; sécurité vérifie prompt injection. |
| Recherche de défaut IA | Critique/red-team. | Le critique cherche hallucination, faux Done ou hypothèse cachée. |
| Désaccord ou contradiction | Escalade orchestrateur puis client si métier. | Design privilégie esthétique, accessibilité bloque contraste. |
| Travail parallèle | Cartes distinctes avec handoff. | Dev implémente, doc prépare guide, QA prépare tests. |

### Format de consultation inter-agent

```yaml
requesting_agent: "developer"
consulted_agent: "ui_designer"
question: "Quel pattern de formulaire respecte la charte et l'accessibilite ?"
context_budget: "tiny"
shared_context:
  - "objectif utilisateur"
  - "extrait charte graphique"
  - "composants existants pertinents"
expected_answer:
  - "recommandation"
  - "contrainte a respecter"
  - "source ou preuve"
  - "impact sur le lot"
expires_after: "fin de carte"
```

## Conformité du contexte par rôle

Chaque rôle reçoit un contexte différent. La conformité se vérifie avant délégation et après handoff.

| Rôle | Contexte minimal obligatoire | Sources à privilégier | Signal de contexte insuffisant |
| --- | --- | --- | --- |
| Analyste besoin | demande, valeur, utilisateurs, contraintes, critères. | brief, tickets, client, docs produit. | user story non testable. |
| Architecte | CDC, contraintes qualité, existant, ADR, risques. | docs architecture, code, C4, décisions. | décision sans compromis explicite. |
| Développeur | carte, fichiers ciblés, conventions, tests liés. | workspace, tests, README, instructions projet. | patch hors scope ou test oublié. |
| UX designer | parcours, personas, états UI, accessibilité, contraintes produit. | brief, wireframes, design system, WCAG. | écran sans état erreur/vide/non autorisé. |
| UI designer | composants, grille, tokens, responsive, accessibilité visuelle. | design system, charte graphique, captures existantes. | visuel incohérent avec composants existants. |
| Direction artistique | marque, ton, palette, iconographie, références créatives. | charte DA, brand book, moodboard, assets validés. | choix esthétique non justifié par la marque. |
| QA | critères, diff, commandes, risques, environnements. | carte, tests, CI, logs, navigateur. | validation impossible à reproduire. |
| Sécurité | données, accès, outils, dépendances, menaces, diff. | threat model, OWASP, config, secrets scanning. | action sensible sans règle d'engagement. |
| Ops | build, CI/CD, env vars, runbook, rollback, observabilité. | CI, Docker, logs, OpenTelemetry, cloud autorisé. | livraison sans rollback ou monitoring. |
| Documentation | public, décisions, livrable, preuves, liens. | docs existantes, ADR, changelog, références. | doc sans public ou sans source. |
| Mémoire | fait stable, source, portée, sensibilité, durée de vie. | handoff validé, journal, décision client. | mémoire sans source ou trop générale. |
| Knowledge janitor | registres, métadonnées, statuts, TTL, embeddings, archives. | sources actives, vector DB, Redis, rapports, handoffs. | vieux rapport utilisé comme source active. |

## Règle de conformité design

Pour toute tâche UI, web design, design system ou direction artistique, la carte n'est pas prête si elle ne précise pas au moins une source de vérité créative : charte graphique, design system, maquette, capture existante, brand book, moodboard validé ou instruction client. Si aucune source n'existe, l'agent doit produire une proposition de direction visuelle à faire valider avant implémentation.

## RACI simplifié

| Activité | Responsable | Approbateur | Consultés | Informés |
| --- | --- | --- | --- | --- |
| Qualifier mission | analyste | client | orchestrateur | subagents utiles |
| Planifier Kanban | orchestrateur | client si priorité métier | QA, sécurité, ops | équipe agentique |
| Préparer contexte | context router | orchestrateur | rôle cible | journal |
| Implémenter | développeur | QA | designer, architecte, sécurité selon cas | client si impact visible |
| Valider UI/DA | designer | client ou DA | dev, QA, accessibilité | orchestrateur |
| Valider sécurité | sécurité | client autorisé ou responsable sécurité | ops, dev | orchestrateur |
| Livrer | orchestrateur | client | QA, sécurité, ops, doc | parties prenantes |
| Capitaliser | mémoire | orchestrateur | sécurité si donnée sensible | équipe agentique |
| Nettoyer connaissances | knowledge janitor | propriétaire de source | orchestrateur, sécurité | équipe agentique |

## Règle finale

L'entreprise-agent ne doit pas être seulement rapide. Elle doit être gouvernable : chaque carte sait qui agit, avec quel accès, quel contexte, quel coût de contexte, quelles preuves, quel validateur et quel prochain passage de relais.
