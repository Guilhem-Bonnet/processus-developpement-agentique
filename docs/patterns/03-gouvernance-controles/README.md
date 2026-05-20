# Patterns de gouvernance et de contrôles

Ces patterns empêchent les actions non autorisées, les choix implicites de modèle et les changements risqués sans simulation ni validation.

La source Mermaid de cette famille est disponible dans [../../../diagrammes/patterns-gouvernance-controles.mmd](../../../diagrammes/patterns-gouvernance-controles.mmd).

## GOV-01 : Policy engine et hooks

| Élément | Description |
| --- | --- |
| Intention | Prévenir les actions non autorisées avant qu'elles se produisent. |
| Problème | Les agents peuvent appeler outils, écrire, pousser ou supprimer au mauvais moment. |
| Solution | Intercepter les moments critiques avec règles allow, block ou escalate. |
| Contrôles | Pre-tool, Pre-write, Pre-release, Pre-dry-run, Incident-detected. |
| Anti-pattern | Revue seulement après exécution. |

## GOV-02 : Dry-run avant action risquée

| Élément | Description |
| --- | --- |
| Intention | Simuler avant d'agir sur un système externe, coûteux ou irréversible. |
| Problème | Un agent peut produire un changement correct localement mais dangereux en contexte réel. |
| Solution | Décrire impact, permissions, coût, rollback, validation et critères de go/no-go. |
| Contrôles | Pre-dry-run, validation humaine, rollback, evidence pack. |
| Anti-pattern | Déploiement, suppression ou appel externe sans simulation. |

## GOV-03 : Hook lifecycle progressif

| Élément | Description |
| --- | --- |
| Intention | Déployer les garde-fous sans casser le flux de travail. |
| Problème | Un hook nouveau peut bloquer trop large ou manquer des cas critiques. |
| Solution | Promouvoir les hooks par modes `shadow`, `canary`, puis `enforced`. |
| Contrôles | Registre des hooks, digest de validation, faux positifs, procédure de retrait. |
| Anti-pattern | Activer un blocage global sans période d'observation. |

## MOD-01 : Model router

| Élément | Description |
| --- | --- |
| Intention | Utiliser le bon modèle pour la bonne tâche. |
| Problème | Le modèle par défaut peut être trop faible, trop cher ou non autorisé. |
| Solution | Router selon tâche, rôle, risque, confidentialité, coût, modalité et evals. |
| Contrôles | Pre-model-route, fallback, evals, logs coût/latence, statut modèle. |
| Anti-pattern | Choix implicite du modèle pour toutes les tâches. |

## GOV-04 : Autonomie gouvernée

| Élément | Description |
| --- | --- |
| Intention | Adapter le niveau d'autonomie de l'agent au risque, aux preuves et aux autorités de validation. |
| Problème | Une autonomie uniforme donne trop de pouvoir aux tâches risquées ou bloque inutilement les tâches simples. |
| Solution | Définir des niveaux d'autonomie par tâche : proposer, préparer, exécuter sous contrôle, exécuter automatiquement, ou bloquer. |
| Contrôles | Policy engine, validation authority, evidence pack, dry-run, incident stop. |
| Anti-pattern | Autonomie maximale par défaut. |

### Niveaux d'autonomie

| Niveau | Comportement | Conditions |
| --- | --- | --- |
| A0 bloqué | L'agent ne peut pas agir. | politique interdite, secret, risque critique non couvert. |
| A1 conseiller | L'agent propose seulement. | besoin flou, décision métier ou sécurité. |
| A2 préparer | L'agent prépare artefacts sans effet externe. | dry-run ou brouillon requis. |
| A3 exécuter avec validation | L'agent agit après accord ou gate. | risque moyen, preuve disponible. |
| A4 exécuter automatiquement | L'agent agit sans validation préalable. | tâche réversible, faible risque, contrôles actifs. |
| A5 auto-améliorer | L'agent peut proposer évolution de règles ou capacités. | gouvernance mature, promotion séparée. |

## MOD-02 : Model retirement guard

| Élément | Description |
| --- | --- |
| Intention | Retirer ou restreindre un modèle sans casser l'orchestration. |
| Problème | Un modèle obsolète peut rester utilisé par habitude ou fallback implicite. |
| Solution | Maintenir statuts active, restricted, deprecated, disallowed et local_only avec fallback explicite. |
| Contrôles | Politique de routage, pre-model-route, eval de remplacement, journal d'appel. |
| Anti-pattern | Laisser un modèle interdit accessible parce qu'il fonctionne encore. |

## Interfaces liées

| Interface | Rôle |
| --- | --- |
| Policy manifest | Déclare règles, permissions, seuils et escalades. |
| Registre des hooks | Trace mode, propriétaire, statut, portée et preuves de validation. |
| Politique de routage LLM | Définit modèle principal, fallback et restrictions par tâche. |
