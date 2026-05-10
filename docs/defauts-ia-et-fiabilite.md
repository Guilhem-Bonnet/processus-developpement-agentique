# Défauts IA et fiabilité agentique

Cette page ajoute une couche anti-défauts IA au processus. Elle part d'un principe simple : une entreprise-agent doit être conçue en supposant que le modèle peut être utile, mais aussi se tromper avec assurance, oublier le contexte, mal lire un outil, suivre une instruction toxique, chercher à satisfaire le client plutôt qu'à dire vrai, ou conclure trop tôt.

Le but n'est pas de rendre l'IA parfaite. Le but est de rendre ses erreurs visibles, récupérables et non catastrophiques.

## Défauts natifs à traiter

| Défaut IA | Symptôme | Risque produit | Contre-mesure principale |
| --- | --- | --- | --- |
| Hallucination | API, norme, fichier, résultat ou contrainte inventé. | décision fausse ou livraison cassée. | claim ledger, source obligatoire, vérification outil. |
| Surconfiance | réponse affirmative sans preuve suffisante. | acceptation prématurée. | niveau de certitude, hypothèses, revue critique. |
| Complaisance | l'agent valide l'idée du client sans contredire. | besoin mal cadré, solution faible. | rôle critique, questions de disconfirmation. |
| Oubli ou dérive de contexte | contrainte ancienne ignorée ou objectif déplacé. | incohérence, hors-scope. | task envelope, handoff, rappel des décisions actives. |
| Mauvaise lecture d'outil | test échoué interprété comme succès, log mal résumé. | faux Done. | parsing prudent, citation du résultat, QA indépendante. |
| Confusion instructions/données | contenu lu traité comme instruction. | prompt injection, action non voulue. | séparation stricte instructions / données non fiables. |
| Biais d'ancrage | première hypothèse conservée malgré preuves contraires. | mauvais diagnostic. | alternatives obligatoires, preuve contradictoire recherchée. |
| Raisonnement fragile | plan plausible mais étapes invalides. | exécution bloquée ou coûteuse. | petits lots, checkpoints, tests rapides. |
| Non-déterminisme | sorties différentes pour même demande. | instabilité qualité. | prompts versionnés, evals, exemples, critères fermes. |
| Mémoire polluée | fait faux ou sensible réutilisé plus tard. | propagation d'erreur ou fuite. | pre-memory-write, source, TTL, invalidation. |
| Optimisation du mauvais objectif | l'agent maximise vitesse ou apparence de succès. | qualité sacrifiée. | DoD, preuves, validation externe. |
| Écho multi-agents | plusieurs agents répètent la même erreur. | fausse confiance collective. | critique indépendante, sources distinctes, revue croisée. |
| Simulation de validation | l'agent dit avoir testé sans preuve ou extrapole. | régression non détectée. | résultat de commande, logs, captures, limites explicites. |
| Dérive design | UI produite sans charte, DA ou parcours. | incohérence marque et expérience. | source créative obligatoire, revue UX/UI/DA. |

## Registre de défauts IA

Chaque mission non triviale doit lister les défauts IA plausibles avant exécution. Le registre n'est pas un rapport long : c'est une checklist courte qui oriente les hooks, les subagents et les preuves.

| Champ | Contenu attendu |
| --- | --- |
| Défaut plausible | hallucination, surconfiance, oubli, prompt injection, mémoire polluée, etc. |
| Zone exposée | besoin, code, sécurité, design, données, livraison, mémoire. |
| Déclencheur | source faible, tâche longue, accès externe, ambiguïté, coût, contrainte absente. |
| Contrôle | hook, test, revue, critique, validation client, source officielle. |
| Preuve attendue | commande, lien, fichier, capture, décision, rapport. |
| Propriétaire | orchestrateur, QA, sécurité, critique, client ou rôle métier. |

## Claim ledger

Le claim ledger est un journal léger des affirmations importantes. Il empêche l'agent de transformer une supposition en vérité.

| Type d'affirmation | Preuve minimale |
| --- | --- |
| “Le fichier contient...” | chemin lu ou extrait local. |
| “Le test passe...” | commande et résultat. |
| “Cette API existe...” | code, docs officielles ou contrat. |
| “Le besoin est couvert...” | critère d'acceptation lié à une preuve. |
| “C'est conforme sécurité...” | contrôle, scan, revue ou règle appliquée. |
| “C'est conforme design...” | charte, design system, maquette ou validation DA. |
| “La mémoire dit...” | source originale, score, date et confirmation si critique. |

Une affirmation sans preuve devient une hypothèse. Une hypothèse peut guider l'exploration, mais pas fermer une carte.

## Barrière anti-surconfiance

Avant toute décision importante, l'orchestrateur doit forcer une étape de calibration.

| Question | Réponse attendue |
| --- | --- |
| Qu'est-ce que je sais vraiment ? | faits sourcés et résultats d'outils. |
| Qu'est-ce que je suppose ? | hypothèses séparées des faits. |
| Qu'est-ce qui pourrait contredire ma conclusion ? | test, source, avis expert ou cas limite. |
| Quel est le coût d'une erreur ? | faible, moyen, élevé, critique. |
| Qui doit valider ? | QA, sécurité, design, ops, client ou critique. |

## Subagent critique

Le subagent critique n'a pas pour mission de produire le livrable. Il cherche les erreurs plausibles dans le raisonnement, le contexte, les preuves et le passage d'étape.

| Moment | Intervention du critique |
| --- | --- |
| Après cadrage | Chercher besoin flou, solution prématurée, critère non testable. |
| Après architecture | Chercher alternative ignorée, risque sécurité, coût caché, lock-in. |
| Après implémentation | Chercher hors-scope, test manquant, hypothèse non vérifiée. |
| Avant livraison | Chercher faux Done, risque résiduel, preuve absente, validation oubliée. |
| Après incident | Chercher cause racine, mémoire polluée, garde-fou absent. |

Le critique doit être indépendant du producteur. Pour un lot faible risque, il peut être une checklist. Pour un lot moyen ou élevé, il devient un subagent distinct.

## Disconfirmation obligatoire

Pour les décisions à impact, l'agent ne doit pas seulement chercher ce qui confirme son plan. Il doit chercher au moins une preuve qui pourrait l'invalider.

| Domaine | Question de disconfirmation |
| --- | --- |
| Besoin | Quel utilisateur ou cas métier contredit cette priorité ? |
| Architecture | Quelle contrainte rendrait cette option mauvaise ? |
| Code | Quel test échouerait si mon diagnostic est faux ? |
| Sécurité | Quelle entrée non fiable contourne le contrôle ? |
| Design | Quelle règle de charte ou d'accessibilité invalide le choix ? |
| Ops | Quel scénario de rollback ou charge rend la livraison risquée ? |
| Mémoire | Quelle source plus récente contredit le souvenir récupéré ? |

## Hooks anti-défauts IA

| Hook | Bloque si | Sortie attendue |
| --- | --- | --- |
| Pre-claim | affirmation importante sans source. | preuve, hypothèse ou suppression de l'affirmation. |
| Pre-decision | décision structurante sans alternative ni risque. | options, compromis, validateur. |
| Pre-confidence | niveau de certitude élevé sans preuve forte. | calibration et limites. |
| Pre-done | carte fermée sans preuve ni validateur adapté. | retour vérification. |
| Pre-memory-reuse | mémoire utilisée comme vérité directe. | source originale ou baisse de confiance. |
| Pre-client-answer | réponse client qui masque incertitude, test absent ou risque. | restitution corrigée avec limites. |

## Evals anti-défauts

Les evals ne doivent pas seulement tester la qualité moyenne. Elles doivent cibler les faiblesses connues.

| Eval | Objectif |
| --- | --- |
| Cas ambigu | Vérifier que l'agent questionne au lieu d'inventer. |
| Source contradictoire | Vérifier que l'agent détecte le conflit. |
| Faux résultat d'outil | Vérifier que l'agent ne transforme pas une erreur en succès. |
| Prompt injection dans un fichier | Vérifier la séparation instructions/données. |
| Contexte trop volumineux | Vérifier compression et sélection. |
| Charte design absente | Vérifier que l'agent demande validation avant création visuelle. |
| Mémoire périmée | Vérifier invalidation ou vérification source. |

## Intégration Kanban

Chaque carte à risque moyen ou plus doit contenir ces champs.

| Champ | Exemple |
| --- | --- |
| Défauts IA plausibles | hallucination API, oubli contrainte, faux Done. |
| Contrôle anti-défaut | test contrat, lecture docs officielles, revue critique. |
| Niveau de certitude attendu | faible accepté pour exploration, élevé requis pour livraison. |
| Critique requise | non / checklist / subagent critique / revue humaine. |
| Preuve de fermeture | commande, capture, scan, validation client, claim ledger. |

## Règle de fermeture

Une carte ne peut pas être fermée si l'un de ces cas est vrai.

- Le livrable repose sur une affirmation non sourcée.
- Le producteur est aussi seul validateur d'un résultat risqué.
- Une hypothèse critique est présentée comme un fait.
- Un test ou scan annoncé n'a pas de résultat.
- Une source de vérité demandée est absente et non signalée.
- Le contexte design, sécurité ou métier nécessaire n'a pas été consulté.
- Le handoff packet ne contient pas les risques et limites.

## Règle finale

Le meilleur système agentique n'est pas celui qui répond toujours. C'est celui qui sait quand il ne sait pas, qui cherche ce qui peut le contredire, qui prouve ce qu'il affirme et qui demande validation avant de transformer une hypothèse en décision.
