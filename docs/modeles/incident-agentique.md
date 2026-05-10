# Modèle de rapport d'incident agentique

## Identification

| Champ | Valeur |
| --- | --- |
| ID incident | A renseigner |
| Date détection | A renseigner |
| Détecté par | hook / QA / sécurité / client / observabilité / agent |
| Mission ou carte | A renseigner |
| Sévérité | faible / moyenne / élevée / critique |
| Statut | ouvert / contenu / corrigé / fermé |

## Description

| Question | Réponse |
| --- | --- |
| Que s'est-il passé ? | A renseigner |
| Quel est l'impact ? | A renseigner |
| Quels systèmes, fichiers, données ou personnes sont touchés ? | A renseigner |
| Quelle action a été stoppée ? | A renseigner |

## Cause racine

| Axe | Analyse |
| --- | --- |
| Défaut IA | hallucination / oubli / surconfiance / faux Done / mémoire polluée / autre |
| Contexte | source absente / périmée / trop large / contradictoire |
| Outil | permission / erreur / sortie mal lue / effet externe |
| Process | hook absent / validation absente / DoD insuffisante |
| Humain | décision manquante / ambiguïté / validation trop rapide |

## Réparation

| Action | Responsable | Preuve | Statut |
| --- | --- | --- | --- |
| A renseigner | A renseigner | A renseigner | à faire / fait |

## Rollback et mémoire

| Surface | Action |
| --- | --- |
| Fichiers / git | A renseigner |
| Redis / cache | A renseigner |
| Vector DB / mémoire | A renseigner |
| Kanban / tickets | A renseigner |
| Secrets / accès | A renseigner |
| Production / externe | A renseigner |

## Prévention

| Changement | Cible | Statut |
| --- | --- | --- |
| nouveau hook / eval / prompt / skill / doc / test | A renseigner | A renseigner |

## Clôture

| Critère | Statut |
| --- | --- |
| Impact compris | oui / non |
| Correction vérifiée | oui / non |
| Mémoire corrigée ou invalidée | oui / non |
| Client/propriétaire informé si nécessaire | oui / non |
| Amélioration créée dans le backlog | oui / non |
