# Norme de structure agentique

## Statut du document

Ce document est le point d'entrée normatif du référentiel. Il distingue le cœur de norme, les templates normatifs et les annexes informatives.

## Objet

La norme définit les exigences minimales pour concevoir, évaluer et auditer une structure agentique gouvernable, vérifiable et maintenable. Elle ne prescrit pas un fournisseur LLM, un framework, un IDE, un runtime ou une infrastructure.

## Langage normatif

| Terme | Sens |
| --- | --- |
| DOIT | Exigence obligatoire pour déclarer la conformité sur le périmètre concerné. |
| NE DOIT PAS | Interdiction normative. |
| DEVRAIT | Exigence recommandée ; tout écart doit être justifié si le risque est significatif. |
| PEUT | Capacité optionnelle ou alternative autorisée. |

## Périmètre normatif

La norme couvre :

- mission, besoin, critères d'acceptation et validation ;
- orchestration, subagents, transitions et délégations ;
- contexte, base de connaissance, mémoire, sources et rétention ;
- routage LLM, providers, coûts, evals et fallback ;
- outils, MCP, navigateur, runtime et workspace ;
- preuves, verdicts, télémétrie, audit et conformité ;
- patterns normatifs et contrôles associés.

La norme ne couvre pas :

- l'implémentation logicielle complète d'un runtime ;
- le choix d'un fournisseur commercial ;
- les obligations juridiques propres à un secteur ;
- les exemples comme source de conformité.

## Structure normative

| Partie | Statut | Document |
| --- | --- | --- |
| Partie 1 - Concepts et périmètre | Normatif | [Modèle de référence](modele-reference-structure-agentique.md), [Terminologie](terminologie-agentique.md) |
| Partie 2 - Exigences | Normatif | [Exigences normatives](exigences-normatives-structure-agentique.md), [Matrice normative maîtresse](matrice-normative-maitresse.md) |
| Partie 3 - Conformité et preuves | Normatif | [Niveaux de conformité](niveaux-conformite-agentique.md), [Matrice de preuves](matrice-preuves-conformite-agentique.md), [Checklist conformité](checklist-evaluation-conformite.md) |
| Partie 4 - Gouvernance | Normatif | [Garde-fous](garde-fous-agentiques.md), [Catalogue des contrôles](catalogue-controles-agentiques.md), [Matrice risques/contrôles/preuves](matrice-risques-controles-preuves.md) |
| Partie 5 - Patterns normatifs | Normatif | [Catalogue des patterns](patterns/README.md), [Matrice patterns/exigences/preuves](patterns/matrice-patterns-exigences-preuves.md), [Relations entre patterns](patterns/relations-patterns.md) |
| Partie 6 - Contrats opérationnels | Template normatif | [Contrats opérationnels](contrats-operationnels-agentiques.md), [Modèles](contrats-operationnels-agentiques.md#templates-disponibles) |
| Annexes | Informatif | [Parcours d'implémentation](parcours-implementation-agentique.md), [Exemples remplis](contrats-operationnels-agentiques.md#exemples-remplis), [Architecture cible issue des références](architecture-cible-reference-agentique.md) |

## Règles de conformité

1. Une structure agentique DOIT déclarer son périmètre de conformité.
2. Une conformité DOIT citer les exigences applicables.
3. Une exigence applicable DOIT avoir une preuve ou une exception documentée.
4. Une exception DOIT avoir justification, risque, owner, contrôle compensatoire et expiration.
5. Un pattern revendiqué DOIT être relié à au moins une exigence et une preuve.
6. Un template vide NE DOIT PAS être considéré comme preuve ; seule une instance remplie et maintenue peut l'être.
7. Une annexe informative PEUT aider l'implémentation mais NE DOIT PAS ajouter d'obligation normative non présente dans le cœur de norme.

## Hiérarchie documentaire

En cas de contradiction :

1. exigences normatives ;
2. matrice normative maîtresse ;
3. niveaux de conformité et matrices de preuves ;
4. contrats opérationnels ;
5. patterns normatifs ;
6. annexes informatives et exemples.

## Livrables minimaux pour déclarer conformité

| Niveau | Livrables minimaux |
| --- | --- |
| N1 Minimal | brief, carte/lot, task envelope, handoff, preuve de fermeture. |
| N2 Contrôlé | registre outils, contrôles essentiels, risques IA, politique secrets. |
| N3 Orchestré | context pack, model routing, workflow manifest, mission ledger. |
| N4 Gouverné | evals, SLO, incident response, rétention, validation authority. |
| N5 Mature | télémétrie corrélée, audit périodique, doc drift, memory integrity, conformité prouvée. |

## Statut documentaire

Le statut de chaque document est défini dans le [registre de statut documentaire](statut-documentaire-norme.md).

