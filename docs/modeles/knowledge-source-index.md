# Modèle de knowledge source index

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Source ID | KSI-... |
| Nom | A renseigner |
| Owner | A renseigner |
| Scope | produit / projet / client / organisation / domaine |
| Statut | candidate / active / archived / superseded / obsolete / sensitive |
| Sensibilité | public / interne / confidentiel / secret / données personnelles |

## Connecteur

| Champ | Valeur |
| --- | --- |
| Type | repo_git / url / api / mcp / database / dossier |
| Localisation | URL, chemin, DSN masqué ou identifiant MCP |
| Authentification | none / token / OAuth / service account / local |
| Mode d'accès | read-only / read-write interdit |
| Périmètre | branches, paths, endpoints, tables ou dossiers autorisés |
| Exclusions | secrets, données personnelles, chemins ou endpoints exclus |

## Indexation

| Champ | Valeur |
| --- | --- |
| Index | lexical / vectoriel / graphe / hybride |
| Chunking | taille, overlap, structure documentaire |
| Métadonnées obligatoires | source_id, version, hash, owner, date, scope, sensitivity |
| Fréquence | webhook / commit / calendrier / manuel / incident |
| Dernière indexation | A renseigner |
| Prochaine revue | A renseigner |

## Contrôles

| Contrôle | Règle |
| --- | --- |
| Pre-index | Vérifier owner, ACL, sensibilité, exclusions et secret scan. |
| Freshness | Bloquer ou dégrader les résultats obsolètes. |
| ACL | Filtrer avant retrieval selon mission, rôle, tenant et modèle autorisé. |
| Source verification | Revenir à la source active pour décision critique. |
| Quarantine | Isoler source inaccessible, suspecte, contaminée ou trop ancienne. |

## Sortie retrieval

| Champ | Valeur |
| --- | --- |
| Extrait | A renseigner |
| Score | A renseigner |
| Source active | lien / commit / endpoint / table / fichier |
| Freshness | fresh / stale / unknown |
| Restrictions | A renseigner |
| Utilisable en contexte ? | oui / non / seulement avec validation |

