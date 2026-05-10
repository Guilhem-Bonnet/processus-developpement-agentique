# Gouvernance des modèles et des connaissances

Cette page couvre deux actifs critiques de l'entreprise-agent : les modèles IA utilisés pour agir et les connaissances que le système récupère, mémorise ou oublie. Le flux détaillé de routage LLM et de rétention/nettoyage est décrit dans [routage-llm-retention-connaissances.md](routage-llm-retention-connaissances.md). L'architecture mémoire complète est définie dans [memoire-hybride-agentique.md](memoire-hybride-agentique.md).

## Gouvernance des modèles

Le choix du modèle est une décision d'architecture. Un modèle rapide, profond, local ou externe n'a pas le même coût, la même latence, la même confidentialité ni le même niveau de raisonnement.

| Critère | Question |
| --- | --- |
| Rôle | Quel subagent ou étape utilise ce modèle ? |
| Capacité | Le modèle doit-il raisonner, coder, classer, résumer, critiquer, visionner ? |
| Risque | Une erreur peut-elle toucher sécurité, production, données ou client ? |
| Confidentialité | Les données peuvent-elles sortir du périmètre local ou organisationnel ? |
| Coût | Quel coût maximal par carte ou par run ? |
| Latence | Quel délai acceptable ? |
| Observabilité | Peut-on tracer usage, coût, erreur et fallback ? |
| Évaluation | Quels cas prouvent que ce modèle convient ? |

## Politique de routage LLM

Le routage doit être explicite dans le task envelope dès qu'une tâche dépasse le simple triage. Le modèle est choisi selon la tâche, le risque, la confidentialité, le coût, les evals et la modalité. Un modèle profond ne compense pas un mauvais contexte ; un modèle rapide ne doit pas traiter une décision durable sans contrôle.

| Décision | Sortie attendue |
| --- | --- |
| Classification de tâche | rôle, complexité, risque, modalité, confidentialité. |
| Choix du modèle | modèle principal, budget, justification. |
| Fallback | modèle alternatif, revue humaine ou suspension. |
| Évaluation | evals passées, seuils et limites connues. |
| Journalisation | coût, latence, tokens, erreurs, divergence. |

## Statuts et retrait des modèles

| Statut | Comportement attendu |
| --- | --- |
| active | utilisable selon politique de routage. |
| restricted | utilisable seulement pour rôles, données ou environnements autorisés. |
| deprecated | utilisable temporairement avec fallback cible et plan de migration. |
| disallowed | rejet obligatoire par pre-model-route ou policy engine. |
| local_only | utilisable uniquement dans un environnement local ou privé. |

Un modèle retiré ne doit pas rester accessible par fallback implicite. Le retrait exige une preuve de remplacement ou une règle de suspension.

## Routage de modèles

| Situation | Modèle recommandé |
| --- | --- |
| Triage, résumé court, classification | modèle rapide et peu coûteux. |
| Cadrage complexe ou architecture | modèle profond avec contexte vérifié. |
| Implémentation ciblée | modèle bon en code, avec tests. |
| Critique/red-team | modèle fort en raisonnement et contradictions. |
| Données sensibles | modèle local ou environnement contractuellement autorisé. |
| Gros volume documentaire | modèle de synthèse plus RAG filtré. |
| Vision ou UI | modèle compatible image si nécessaire, plus sources design. |

## Politique de fallback

| Déclencheur | Réponse |
| --- | --- |
| Modèle indisponible | basculer vers modèle autorisé ou suspendre. |
| Coût trop élevé | réduire contexte, utiliser résumé, demander validation. |
| Réponse instable | relancer avec prompt plus strict ou critique indépendante. |
| Échec eval critique | bloquer release agentique. |
| Données sensibles détectées | arrêter et router vers modèle/localité autorisée. |
| Divergence entre modèles | escalader au critique ou au client selon domaine. |

## Cycle de vie des connaissances

| Étape | Règle |
| --- | --- |
| Création | Une connaissance vient d'une source identifiable ou d'une décision validée. |
| Qualification | Elle reçoit type, propriétaire, date, portée, sensibilité et durée de vie. |
| Indexation | Elle est indexée seulement si elle est utile, stable et non sensible. |
| Récupération | Elle est filtrée par métadonnées avant similarité. |
| Vérification | Pour décision critique, revenir à la source de vérité. |
| Mise à jour | Réindexer après changement de version, ADR, charte, API ou incident. |
| Expiration | TTL ou date de revue pour éviter mémoire périmée. |
| Suppression | Purger secrets, données personnelles inutiles, faits faux ou obsolètes. |

## Mémoire hybride

| Couche | Rôle |
| --- | --- |
| Redis chaud | état court, cache, verrou, file d'événements. |
| Mémoire vectorielle | rappel sémantique de sources durables. |
| Graphe de connaissances | relations entre missions, tâches, décisions, preuves et sources. |
| Sidecar structuré | faits temporels, validité, confiance et provenance. |
| Journal append-only | historique des transitions et décisions. |
| Source registry | statut actif, archivé, remplacé, obsolète ou sensible. |

Le vectoriel rappelle, le graphe relie, le sidecar qualifie et la source de vérité décide.

## Rétention et nettoyage documentaire

La production agentique crée naturellement beaucoup d'artefacts : rapports, handoffs, traces, captures, diagnostics, brouillons, incidents et résumés. Tous ne doivent pas être conservés ni indexés. Le nettoyage doit être actif, comme une politique de rétention de logs appliquée à la connaissance.

| Destination | Usage |
| --- | --- |
| Source active | fait foi pour les décisions. |
| Mémoire durable | connaissance stable, sourcée, réutilisable. |
| Archive | historique consultable, non prioritaire pour le contexte. |
| Rétention courte | utile temporairement, TTL obligatoire. |
| Désindexation | retirer de la recherche vectorielle sans forcément supprimer le fichier. |
| Purge | supprimer ce qui est faux, sensible, inutile ou expiré. |

## Knowledge janitor

Le knowledge janitor est le rôle chargé de garder le corpus maintenable. Il détecte les vieux rapports, doublons, documents remplacés, sources sans propriétaire, embeddings obsolètes et mémoires contaminées. Il propose ensuite de conserver, résumer, archiver, désindexer ou purger.

## Métadonnées minimales

| Métadonnée | Usage |
| --- | --- |
| source | Retrouver la vérité originale. |
| type | brief, ADR, code, test, charte, incident, ticket, doc officielle. |
| projet | Éviter mélange entre missions. |
| version | Gérer changements et obsolescence. |
| date | Évaluer fraîcheur. |
| propriétaire | Savoir qui peut valider ou corriger. |
| sensibilité | Bloquer indexation ou récupération interdite. |
| score de confiance | Aider le routeur de contexte. |
| TTL | Forcer revue ou expiration. |
| valid_until | Définir la date de revue ou d'expiration. |
| status | active, archived, superseded, obsolete, sensitive. |
| superseded_by | Pointer vers la source plus récente. |
| indexable | Dire si la source peut entrer en vector DB. |
| retention_class | durable, projet, mission, court terme ou purge. |

## Conflits de connaissances

| Conflit | Réponse |
| --- | --- |
| Source plus récente contredit mémoire | privilégier source récente, invalider mémoire. |
| Documentation contredit code | lire tests/CI, demander arbitrage si métier. |
| Charte contredit demande ponctuelle | escalader client ou DA. |
| ADR contredit implémentation | créer carte d'analyse architecture. |
| Deux tickets se contredisent | demander décision produit. |
| Vector DB donne résultat similaire mais mauvais projet | filtrer par métadonnées, corriger index. |

## Règles de mémoire

- Ne jamais mémoriser un secret ou une donnée personnelle inutile.
- Ne pas mémoriser une hypothèse comme un fait.
- Préférer une note courte, sourcée et portée limitée.
- Invalider après incident, changement de charte, migration ou release majeure.
- Relier toute mémoire durable à une décision, une source ou un handoff validé.
- Désindexer les sources obsolètes, remplacées ou sensibles.
- Nettoyer périodiquement les rapports temporaires, traces et handoffs non durables.

## Règle finale

La mémoire augmente la puissance de l'agent seulement si elle sait oublier. Une connaissance sans source, sans propriétaire ou sans date devient rapidement une dette.
