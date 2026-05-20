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

## Interfaces liées

| Interface | Rôle |
| --- | --- |
| Registre des surfaces runtime | Inventorie agents, skills, hooks, workflows, traces et artefacts. |
| Registre des capacités dynamiques | Suit promotion, expiration, propriétaire et preuves. |
| Politique de rétention | Détermine ce qui devient durable, archive, TTL ou purge. |
