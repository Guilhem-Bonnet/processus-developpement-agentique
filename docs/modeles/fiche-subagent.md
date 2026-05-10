# Modèle de fiche subagent

## Identité

| Champ | Valeur |
| --- | --- |
| Nom du subagent | A renseigner |
| Rôle | analyste / architecte / dev / UX / UI / DA / QA / sécurité / critique / ops / doc / mémoire |
| Propriétaire | A renseigner |
| Version du prompt | A renseigner |
| Niveau de risque maximal | faible / moyen / élevé / critique |

## Mission

| Élément | Valeur |
| --- | --- |
| Responsabilité principale | A renseigner |
| Hors périmètre | A renseigner |
| Entrées attendues | task envelope, sources, critères, outils |
| Sorties attendues | handoff packet, preuves, risques, prochain trigger |
| Validateur | A renseigner |

## Contexte

| Champ | Valeur |
| --- | --- |
| Budget par défaut | tiny / small / medium / deep |
| Sources obligatoires | A renseigner |
| Sources interdites | A renseigner |
| Mémoire autorisée | oui / non, conditions |
| Signaux de contexte insuffisant | A renseigner |

## Outils

| Outil | Autorisé | Conditions |
| --- | --- | --- |
| lecture | oui / non | A renseigner |
| édition | oui / non | A renseigner |
| terminal | oui / non | A renseigner |
| navigateur | oui / non | A renseigner |
| MCP | oui / non | A renseigner |
| réseau | oui / non | A renseigner |

## Garde-fous

| Risque | Garde-fou |
| --- | --- |
| hallucination | source obligatoire ou hypothèse |
| surconfiance | niveau de certitude et critique |
| hors-scope | task envelope strict |
| données sensibles | refus ou procédure dédiée |
| faux Done | preuve vérifiable |

## Evals

| Eval | Seuil |
| --- | --- |
| A renseigner | A renseigner |

## Historique

| Version | Changement | Validation |
| --- | --- | --- |
| 0.1 | création | A renseigner |
