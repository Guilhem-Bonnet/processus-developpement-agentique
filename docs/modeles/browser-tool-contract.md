# Modèle de browser tool contract

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Browser Tool ID | BTW-... |
| Owner | A renseigner |
| Scope | mission / projet / domaine |
| Statut | draft / active / restricted / retired |

## Périmètre

| Champ | Valeur |
| --- | --- |
| URLs autorisées | A renseigner |
| URLs interdites | A renseigner |
| Authentification | none / session utilisateur / compte test |
| Actions autorisées | navigate / click / type / upload / download / screenshot |
| Actions interdites | achat / suppression / publication / paiement / production |

## Preuves visuelles

| Preuve | Quand |
| --- | --- |
| DOM snapshot | avant action risquée et avant verdict. |
| Screenshot | état initial, état final, anomalie visuelle. |
| UI state trace | séquence action -> observation -> résultat. |
| Console/network logs | erreur ou intégration critique. |

## Contrôles

| Contrôle | Règle |
| --- | --- |
| Blast radius | limiter domaine, session, données et effets externes. |
| Dry-run | obligatoire pour action irréversible ou production. |
| Validation | design authority ou validation humaine si achat/publication/suppression. |

