# Modèle d'eval dataset record

## Métadonnées

| Champ | Valeur |
| --- | --- |
| Dataset ID | EVAL-... |
| Nom | A renseigner |
| Owner | A renseigner |
| Version | A renseigner |
| Scope | prompt / modèle / workflow / skill / retrieval |

## Cas d'évaluation

| Case ID | Entrée | Sortie attendue | Juge | Seuil | Risque couvert |
| --- | --- | --- | --- | --- | --- |
| A renseigner | A renseigner | A renseigner | humain / LLM / règle | A renseigner | A renseigner |

## Lifecycle

| Événement | Règle |
| --- | --- |
| ajout cas | source, raison et risque liés. |
| changement prompt/modèle | rejouer dataset critique. |
| échec | bloquer promotion ou ouvrir incident. |
| dérive | mettre à jour seuil ou retirer modèle/prompt. |

