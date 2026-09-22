# Concevoir, développer, tester, sécuriser et déployer une application métier avec l'IA

**Une formation pratique à Replit et au développement assisté par l'IA, appliquée aux RH, à la finance et au service client.**

---

## Présentation

Cette formation apprend à transformer un besoin métier en application fonctionnelle, en utilisant [Replit](https://replit.com) et son Agent IA. Elle ne se limite pas à « générer une application avec l'IA » : elle apprend à **concevoir, tester, sécuriser, déployer et documenter** cette application, pour que ce qui est produit soit fiable et défendable, pas seulement impressionnant en démonstration.

Trois mises en situation métier — recrutement, comptabilité, service client — servent de fil conducteur : la même méthode y est appliquée à trois problèmes différents, jusqu'à un projet final où chaque participant l'applique à un besoin de son choix.

## Public et prérequis

- **Public** : étudiants de Master et professionnels des RH, de la finance et du service client, ou toute personne souhaitant automatiser des tâches métier sans savoir programmer.
- **Prérequis** : aucun en programmation. Le code généré par l'IA est lu et compris, pas écrit à la main.
- **Matériel** : un ordinateur, une connexion internet, un compte Replit avec l'Agent et le déploiement activés.

## Durée et format

- **21 heures** au total : 3 journées de 7 h, ou 6 demi-journées.
- **Méthode** : formation par projets. Un apport théorique court précède chaque mise en pratique ; l'essentiel du temps est passé à construire, tester et corriger de vraies applications.
- **Répartition** : environ 19 % de théorie, 73 % de pratique, 8 % de discussion.

## Ce que vous saurez faire à l'issue de la formation

- Expliquer l'architecture d'une application IA (front-end, back-end, base de données, API, LLM, secrets, flux utilisateur).
- Transformer un besoin métier en cahier des charges, user stories et workflow, avant de construire quoi que ce soit.
- Construire une application avec Replit Agent par instructions successives, en lisant la logique du code généré.
- Tester et déboguer une application IA : tests métier, tests adversariaux, hallucinations, injection de prompt.
- Sécuriser et gouverner une application : données, secrets, authentification, RGPD, validation humaine, traçabilité.
- Déployer, documenter et défendre une application, en justifiant ses choix et en nommant ses limites.

## La progression pédagogique

Chaque module et chaque lab suivent la même logique en sept phases :

```text
Comprendre → Construire → Tester → Corriger → Sécuriser → Déployer → Documenter
```

Cette progression distingue la formation du simple « vibe coding » (décrire, générer, ajuster) : l'objectif est d'apprendre le **développement assisté par l'IA**, où l'on analyse le besoin, on décompose, on construit progressivement, on lit le code généré, on teste, on sécurise et on documente — en passant du rôle de simple utilisateur d'un outil à celui de chef de projet et de contrôleur qualité.

## Programme, module par module

| # | Module | Durée | Ce qu'on y fait |
|---|---|---|---|
| 1 | **Découvrir Replit et l'IA générative** | 2 h | L'interface, l'Agent, le cycle de travail, l'anatomie d'un bon prompt. |
| 2 | **Concevoir une application avec l'IA** | 2 h | Passer d'un besoin métier à un cahier des charges, un workflow et un plan de développement. |
| 3 | **Lab RH — tri des CV** | 3 h | Une application qui note les CV avec une grille explicite et une décision humaine finale. |
| 4 | **Lab Finance — assistant comptable** | 3 h | Un pipeline qui nettoie, classe et vérifie des transactions, jusqu'à un rapport de clôture. |
| 5 | **Lab Service client — CRM, chatbot, RAG** | 3 h 30 | Un chatbot qui recherche avant de répondre, avec validation humaine avant tout envoi. |
| 6 | **Tester et déboguer une application IA** | 2 h 30 | Atelier « Quand l'IA se trompe », tests métier et tests adversariaux. |
| 7 | **Sécurité, gouvernance et déploiement** | 2 h | Données, secrets, authentification, RGPD, traçabilité, mise en ligne. |
| 8 | **Projet final** | 3 h | Chaque participant applique la méthode complète à un problème de son choix, avec soutenance. |

## Les trois labs métier

Chaque lab suit la même structure : un scénario, un objectif, une construction pas à pas par instructions à l'Agent, une phase de tests sur des cas piégés, une étape de validation humaine, et une documentation finale.

- **Lab RH** : au-delà du tri, l'accent est mis sur une note **expliquée** critère par critère, et sur les biais à surveiller (âge, genre, origine) ainsi que sur les obligations liées aux données personnelles.
- **Lab Finance** : un pipeline complet, du nettoyage des données jusqu'au tableau de bord, avec une détection d'anomalies testée sur des cas volontairement erronés.
- **Lab Service client** : introduction au **RAG** (rechercher avant de répondre) et au principe du **human-in-the-loop** : aucune réponse ne part au client sans validation d'un agent humain.

## Le projet final

Chaque participant, seul ou en groupe, choisit un problème métier de son choix et applique la méthode complète : cahier des charges, construction avec une fonctionnalité IA, tests, sécurisation, déploiement, documentation, puis une soutenance de 5 à 10 minutes où il doit pouvoir répondre à trois questions : pourquoi cette architecture, comment il l'a testée, et quelles en sont les limites.

## Contenu du dépôt

| Fichier | Contenu |
|---|---|
| `presentation.html` | Support de présentation complet des 8 modules, à ouvrir dans un navigateur. |
| `LAB1_RH.md` | Guide pas à pas du lab RH (module 3). |
| `LAB2_FINANCE.md` | Guide pas à pas du lab Finance (module 4). |
| `LAB3_SERVICE_CLIENT.md` | Guide pas à pas du lab Service client (module 5). |
| `PROJET_FINAL.md` | Guide pas à pas du projet final (module 8). |

## Matériel à prévoir pour animer la formation

- Comptes Replit actifs avec l'Agent et le déploiement activés.
- Données fictives : CV et fiche de poste (Lab RH), relevé bancaire et factures (Lab Finance), FAQ d'entreprise (Lab Service client).
- Une application contenant 5 erreurs volontaires, pour l'atelier de débogage du module 6.
