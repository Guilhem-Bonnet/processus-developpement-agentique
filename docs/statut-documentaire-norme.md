# Statut documentaire de la norme agentique

Ce registre classe les documents selon leur rôle normatif. Il évite de confondre exigence, guide, exemple, audit ou template.

## Catégories

| Catégorie | Définition | Peut créer une obligation ? |
| --- | --- | --- |
| Normatif | Définit exigences, interdictions, niveaux, contrôles ou preuves. | oui |
| Template normatif | Modèle d'artefact attendu par la norme. | oui, si le template est requis par une exigence |
| Informatif | Explique, illustre ou propose un chemin d'application. | non |
| Audit / source | Documente les références, analyses ou plans de récupération. | non, sauf si repris par un document normatif |

## Registre

| Document | Catégorie | Rôle |
| --- | --- | --- |
| `norme-structure-agentique.md` | Normatif | Point d'entrée et hiérarchie documentaire. |
| `terminologie-agentique.md` | Normatif | Définitions des termes. |
| `modele-reference-structure-agentique.md` | Normatif | Plans, composants et interfaces minimales. |
| `exigences-normatives-structure-agentique.md` | Normatif | Exigences AG-* obligatoires/recommandées. |
| `matrice-normative-maitresse.md` | Normatif | Table maîtresse exigence -> profil -> preuve -> pattern -> contrôle. |
| `niveaux-conformite-agentique.md` | Normatif | Niveaux N0 à N5 et critères de conformité. |
| `matrice-preuves-conformite-agentique.md` | Normatif | Preuves acceptables par domaine. |
| `catalogue-controles-agentiques.md` | Normatif | Contrôles CTRL-* et triggers. |
| `matrice-risques-controles-preuves.md` | Normatif | Risques, contrôles, preuves et télémétrie. |
| `garde-fous-agentiques.md` | Normatif | Garde-fous transverses, DoR, DoD et hooks. |
| `patterns/README.md` | Normatif | Catalogue des patterns. |
| `patterns/matrice-patterns-exigences-preuves.md` | Normatif | Couverture patterns -> exigences -> preuves. |
| `patterns/relations-patterns.md` | Normatif | Dépendances entre patterns. |
| `patterns/matrice-maturite-patterns.md` | Normatif | Profil d'entrée des patterns. |
| `contrats-operationnels-agentiques.md` | Template normatif | Registre des contrats et templates. |
| `docs/modeles/*.md` | Template normatif | Modèles d'artefacts à instancier. |
| `audit-conformite-agentique.md` | Normatif | Méthode d'audit et décision de conformité. |
| `checklist-evaluation-conformite.md` | Normatif | Checklist d'évaluation. |
| `gestion-exceptions-conformite.md` | Normatif | Gestion des exceptions. |
| `modele-tracabilite-agentique.md` | Normatif | Traçabilité exigence/contrôle/preuve/verdict. |
| `observabilite-telemetrie-agentique.md` | Normatif | Signaux minimaux de télémétrie. |
| `observabilite-evals-slo-agentiques.md` | Normatif | Evals, SLO et scorecards. |
| `profils-preuves-par-tache.md` | Normatif | Preuves par type de tâche. |
| `parcours-implementation-agentique.md` | Informatif | Chemin d'adoption progressif. |
| `modeles/exemples/*.md` | Informatif | Exemples remplis non obligatoires. |
| `architecture-cible-reference-agentique.md` | Informatif | Synthèse issue des références. |
| `plan-ajouts-conception-agentique.md` | Audit / source | Historique de consolidation et backlog. |
| `references-agentiques.md` | Audit / source | Références et inspirations. |

## Règle de promotion

Un contenu informatif devient normatif seulement s'il est repris explicitement dans une exigence AG-*, un contrôle CTRL-* ou une matrice normative.

