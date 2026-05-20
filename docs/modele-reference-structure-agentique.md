# Modèle de référence d'une structure agentique

Ce modèle décrit la base d'une structure agentique qui fonctionne. Il ne prescrit pas un fournisseur, un framework ou un produit : il définit les plans, composants et contrats qui doivent exister pour qu'une organisation d'agents soit pilotable, vérifiable et maintenable.

## Périmètre

Le modèle couvre :

- la relation client utilisateur / entreprise-agent ;
- l'orchestration des rôles agentiques ;
- la gestion du contexte et de la mémoire ;
- le routage des modèles ;
- la gouvernance des outils et intégrations ;
- les garde-fous, preuves, validations et incidents ;
- la capitalisation et le nettoyage des connaissances.

Le modèle ne couvre pas :

- le choix obligatoire d'un fournisseur LLM ;
- l'implémentation détaillée d'un runtime agentique ;
- les règles juridiques propres à chaque organisation ;
- les SLA contractuels d'un produit commercial.

## Plans normatifs

| Plan | Fonction | Exigence centrale |
| --- | --- | --- |
| Mission | Transformer un signal client en travail qualifié. | Toute mission DOIT avoir objectif, périmètre, critères et validateur. |
| Orchestration | Décider qui agit, quand, avec quoi. | Toute délégation DOIT passer par un task envelope. |
| Contexte | Fournir juste assez d'information sourcée. | Toute source critique DOIT être fraîche, traçable et qualifiée. |
| Capacités | Donner aux agents prompts, skills, outils et modèles. | Toute capacité risquée DOIT être gouvernée par permission et preuve. |
| Gouvernance | Encadrer accès, coûts, risques et validations. | Toute action sensible DOIT avoir une autorité de validation. |
| Qualité | Vérifier le résultat par preuves. | Tout Done DOIT être démontré par test, revue, rendu, trace ou décision. |
| Mémoire | Garder ce qui est durable et oublier le reste. | Toute mémoire durable DOIT être stable, sourcée, non sensible et révisable. |

## Composants obligatoires

| Composant | Rôle minimal | Entrées | Sorties |
| --- | --- | --- | --- |
| Interface de mission | Capturer besoin, contraintes et décisions client. | demande, contexte, priorités | brief agentique |
| Orchestrateur | Qualifier, planifier, déléguer et synthétiser. | brief, Kanban, règles | cartes, task envelopes, décisions |
| Policy engine | Autoriser, bloquer ou escalader. | tâche, risques, permissions | décision allow/block/escalate |
| Context router | Sélectionner le contexte pertinent. | mission, rôle, budget | contexte minimal sourcé |
| Orchestrateur de contexte avancé | Arbitrer profils, budgets, couches mémoire, exclusions et persistance. | mission, sources, mémoire, politiques | context pack, scorecard, décision de rétention |
| Model router | Choisir le modèle adapté. | tâche, risque, coût, confidentialité | modèle principal, fallback |
| Tool registry | Gouverner les outils. | inventaire, scopes, risques | outils autorisés par tâche |
| Hook engine | Intercepter moments critiques. | événements, politiques | blocage, alerte, journal |
| Subagents | Exécuter des rôles spécialisés. | task envelope | handoff packet |
| Evidence journal | Tracer lectures, actions, décisions et preuves. | outils, agents, validations | journal auditables |
| Eval harness | Mesurer prompts, modèles et workflows. | cas, sorties, critères | score, régression, décision |
| Knowledge janitor | Maintenir la qualité du corpus. | sources, TTL, statuts | archive, purge, désindexation |

## Interfaces minimales

| Interface | Producteur | Consommateur | Obligation |
| --- | --- | --- | --- |
| Brief agentique | client / orchestrateur | orchestrateur | décrire le besoin et les contraintes. |
| Carte Kanban | orchestrateur | équipe agentique | porter état, contexte, risques, modèles et preuves. |
| Context pack | orchestrateur de contexte | subagent / étape | transmettre sources vérifiées, exclusions, contraintes et confiance. |
| Task envelope | orchestrateur | subagent | limiter objectif, outils, contexte et sortie. |
| Handoff packet | subagent | orchestrateur | transmettre résultat, preuves, hypothèses, risques. |
| Claim ledger | producteur | QA / critique | relier affirmation et preuve. |
| Dossier d'acceptation | orchestrateur | client | permettre acceptation ou refus éclairé. |
| Rapport d'incident | détecteur | gouvernance | contenir, corriger et prévenir. |
| Pattern record | architecte / gouvernance | référentiel agentique | suivre statut, maturité, exigences et preuves d'un pattern. |

## Cycle de fonctionnement

1. Un signal client est qualifié en mission.
2. La mission est transformée en exigences, risques et critères.
3. L'orchestrateur crée ou met à jour les cartes Kanban.
4. Le context router sélectionne les sources pertinentes.
5. Le model router choisit le modèle et le fallback.
6. Le policy engine autorise ou bloque les actions.
7. Les subagents exécutent des lots limités par task envelope.
8. Les résultats sont vérifiés par preuves, evals, hooks et validations.
9. Le livrable est accepté, refusé ou remis en correction.
10. Les connaissances sont capitalisées, archivées, désindexées ou purgées.

## Règles structurelles

- Une structure agentique NE DOIT PAS confondre conversation et pilotage.
- Un agent NE DOIT PAS être son seul validateur sur une décision métier, sécurité ou architecture durable.
- Un outil externe NE DOIT PAS être appelé sans politique d'accès, journalisation et périmètre.
- Une mémoire NE DOIT PAS devenir durable sans source, propriétaire, portée, sensibilité et durée de vie.
- Une base vectorielle NE DOIT PAS être considérée comme source de vérité.
- Un modèle LLM NE DOIT PAS être choisi implicitement pour une tâche à risque.
- Un livrable NE DOIT PAS être accepté sans preuve proportionnée au risque.

## Profils d'implémentation

| Profil | Description |
| --- | --- |
| Minimal | Orchestrateur, Kanban, task envelope, handoff, preuves. |
| Contrôlé | Ajoute policy engine, hooks, permissions, claim ledger. |
| Orchestré | Ajoute subagents spécialisés, context router, model router. |
| Gouverné | Ajoute evals, SLO, incidents, rétention, validation authority. |
| Mature | Ajoute observabilité complète, red teaming, amélioration continue et audit de mémoire. |
