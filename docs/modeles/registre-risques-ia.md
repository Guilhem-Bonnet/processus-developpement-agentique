# Modèle de registre des risques IA

| ID | Risque IA | Zone exposée | Déclencheur | Contrôle | Propriétaire | Statut |
| --- | --- | --- | --- | --- | --- | --- |
| RIA-001 | hallucination / oubli / surconfiance / faux Done / prompt injection | besoin / code / design / sécurité / ops / mémoire | A renseigner | hook / test / critique / validation | A renseigner | ouvert / contrôlé / accepté / fermé |

## Risques fréquents à considérer

| Risque | Symptôme | Contrôle recommandé |
| --- | --- | --- |
| Routage LLM inadapté | modèle trop faible, trop coûteux ou non autorisé. | politique de routage, evals, fallback. |
| Source obsolète | l'agent cite un vieux rapport ou une décision remplacée. | statut active/superseded, valid_until, Pre-context-reuse. |
| Pollution vectorielle | résultats RAG dominés par brouillons, handoffs ou rapports périmés. | Pre-index, désindexation, knowledge janitor. |
| Accumulation documentaire | le projet devient trop gros pour savoir quoi croire. | registre de rétention, archive, purge périodique. |
| Mémoire durable fausse | une erreur est réutilisée dans plusieurs missions. | purge mémoire, incident, correction source, eval de non-régression. |
| Donnée sensible indexée | secret ou donnée personnelle ressort dans une recherche. | classification, non-indexation, purge et audit. |

## Évaluation

| Champ | Valeur |
| --- | --- |
| Probabilité | faible / moyenne / élevée |
| Impact | faible / moyen / élevé / critique |
| Gravité | faible / moyenne / élevée / critique |
| Preuve attendue | A renseigner |
| Critique requise | non / checklist / subagent / humain |
| Décision client nécessaire | oui / non |

## Revue

| Question | Réponse |
| --- | --- |
| Quels risques bloquent le passage d'étape ? | A renseigner |
| Quels risques sont acceptés explicitement ? | A renseigner |
| Quels contrôles doivent devenir permanents ? | A renseigner |
| Quelles sources doivent être désindexées ou purgées ? | A renseigner |
