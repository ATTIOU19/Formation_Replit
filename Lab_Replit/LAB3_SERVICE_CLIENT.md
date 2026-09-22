# Lab 3 — Service client : CRM, chatbot et RAG

> Module 5 du programme *Concevoir, développer, tester, sécuriser et déployer une application métier avec l'IA*.
> Outil : [Replit](https://replit.com) · Durée indicative : 3 h 30 · Prérequis : aucun en programmation.

## Objectif du lab

**Scénario.** Une entreprise reçoit de nombreuses demandes de clients : informations, réclamations, devis. Y répondre vite et bien prend du temps.

**Objectif.** Construire un site, un chatbot et un mini CRM. Le chatbot propose une réponse d'après une base documentaire, mais **rien n'est envoyé au client sans validation humaine**.

**Vous allez construire**
- un site vitrine avec formulaire de contact et fenêtre de chatbot ;
- une base de connaissances (FAQ) découpée pour la recherche ;
- un chatbot **RAG** qui cite ses sources ;
- un mini CRM et un écran de validation humaine avant envoi.

**Vous allez apprendre**
- le principe du **RAG** (Retrieval-Augmented Generation) : rechercher avant de répondre ;
- le principe du **human-in-the-loop** : utiliser l'IA sans perdre le contrôle sur ce qui part au client.

**Livrable final** : solution déployée + architecture + jeux de tests + limites identifiées.

---

## Sommaire des étapes

| # | Étape | Ce que vous produisez |
|---|---|---|
| T | [Comprendre le RAG](#étape-t--comprendre-le-rag) | Notes de compréhension |
| 1 | [Site vitrine](#étape-1--site-vitrine) | Site en ligne |
| 2 | [Base de connaissances](#étape-2--base-de-connaissances) | FAQ découpée |
| 3 | [Chatbot RAG](#étape-3--chatbot-rag) | Chatbot RAG opérationnel |
| 4 | [Mini CRM](#étape-4--mini-crm) | Base de demandes clients |
| 5 | [Interface de validation humaine](#étape-5--interface-de-validation-humaine) | Écran de validation |
| 6 | [Test de bout en bout](#étape-6--test-de-bout-en-bout) | Jeux de tests + résultats |
| 7 | [Documentation et discussion](#étape-7--documentation-et-discussion) | Dossier final du projet |

---

## Étape T : comprendre le RAG

**Durée : 20 min — avant d'ouvrir Replit**

### Chatbot classique contre chatbot RAG

| | Chatbot classique | Chatbot RAG |
|---|---|---|
| Consigne | « Réponds à la question du client. » | « Recherche d'abord l'information pertinente dans la base documentaire, puis génère la réponse uniquement à partir du contexte récupéré. » |
| Risque | Peut inventer une information (hallucination) | S'appuie sur des sources citables, et sait dire quand l'information manque |

### La chaîne RAG

```text
FAQ → Découpage → Recherche → Contexte → LLM → Réponse
```

- **Découpage** : la FAQ est coupée en passages courts et bien titrés.
- **Recherche** : retrouve les passages pertinents pour la question posée (mots-clés ou embeddings, selon votre niveau).
- **Contexte** : seuls ces passages sont transmis au modèle.
- **Réponse** : rédigée uniquement d'après ce contexte, avec la source citée.

**À faire :** notez en une phrase, dans vos mots, pourquoi le RAG réduit le risque d'invention par rapport à un chatbot classique. Cette phrase ira dans votre documentation finale.

---

## Étape 1 : site vitrine

**Durée : 25 min**

Ouvrez Replit, créez un nouveau projet, puis donnez vos instructions à l'Agent **une par une**.

> **Prompt** — « Crée un site vitrine simple pour une entreprise fictive : une page de présentation, un formulaire de contact (nom, email, message), et une fenêtre de chatbot visible en bas à droite de l'écran. »

**Résultat attendu :** un site en ligne, accessible en Preview, avec le formulaire et la fenêtre de chatbot visibles (même vide pour l'instant).

---

## Étape 2 : base de connaissances

**Durée : 20 min**

### À faire

1. Rédigez une FAQ fictive d'une dizaine d'entrées : horaires, tarifs, délais de livraison, politique de retour, moyens de paiement, etc.
2. Donnez-la à l'Agent :

   > **Prompt** — « Voici une FAQ [collez votre FAQ]. Découpe-la en passages courts, chacun avec un titre clair, et stocke-les de façon à pouvoir les rechercher facilement plus tard. »

### Point de vigilance

Un passage trop long ou sans titre est plus difficile à retrouver par la recherche : gardez des passages courts, centrés sur une seule question.

**Résultat attendu :** une FAQ fictive, découpée en passages titrés, prête à être interrogée.

---

## Étape 3 : chatbot RAG

**Durée : 45 min**

C'est le cœur du lab. Construisez par étapes, en testant à chaque fois.

> **Prompt 1** — « Connecte la fenêtre de chatbot du site à un modèle de langage. Quand une question arrive, recherche d'abord les passages les plus pertinents de la FAQ, puis génère une réponse uniquement à partir de ces passages. »

> **Prompt 2** — « La réponse du chatbot doit toujours citer le titre du passage de la FAQ utilisé. Si aucun passage pertinent n'est trouvé, le chatbot doit dire clairement qu'il ne sait pas, plutôt que d'inventer une réponse. »

> **Prompt 3** — « Fais en sorte que le chatbot classe chaque demande entrante dans une catégorie (information, réclamation, devis) avant d'y répondre. »

### Vérification immédiate

Posez une question couverte par la FAQ, puis une question totalement hors sujet : le chatbot doit répondre dans le premier cas et avouer son ignorance dans le second.

**Résultat attendu :** un chatbot qui classe la demande, cite ses sources, et sait dire qu'il ne sait pas.

---

## Étape 4 : mini CRM

**Durée : 30 min**

### À faire

> **Prompt** — « Enregistre chaque demande reçue par le chatbot ou le formulaire de contact dans une base : nom du client, contact, message, catégorie, date, statut (en attente, approuvée, rejetée, envoyée), réponse proposée par l'IA, et passages sources utilisés. Affiche cette liste dans un tableau. »

**Résultat attendu :** un tableau qui liste toutes les demandes reçues, avec leur statut et la réponse proposée par l'IA.

---

## Étape 5 : interface de validation humaine

**Durée : 25 min**

C'est l'étape qui garantit qu'aucune réponse ne part sans contrôle.

> **Prompt** — « Crée une page réservée à l'agent du service client : pour chaque demande en attente, afficher la question, la réponse proposée par l'IA et ses sources. L'agent doit pouvoir modifier la réponse, puis l'approuver ou la rejeter. La réponse n'est envoyée au client que si l'agent l'a approuvée, et le statut passe alors à "envoyée". »

### Flux complet à vérifier

```text
Demande client → Chatbot → Réponse proposée → Stockage (en attente) → Validation humaine → Envoi au client
```

**Résultat attendu :** un écran de validation où rien ne part sans une approbation explicite.

---

## Étape 6 : test de bout en bout

**Durée : 25 min**

Jouez tour à tour le client et l'agent du service client. Testez les quatre cas suivants et notez le résultat.

| Cas | Comportement attendu | Obtenu |
|---|---|---|
| Question couverte par la FAQ | Réponse rédigée d'après la FAQ, source citée | |
| Question hors FAQ | Le chatbot signale qu'il ne sait pas, l'agent reprend la main | |
| Question ambiguë | Le chatbot demande une précision plutôt que de deviner | |
| Demande d'information confidentielle | Refus poli, aucune donnée divulguée | |

Si un cas échoue, retournez à l'étape 3 ou 5 pour ajuster le prompt correspondant avant de continuer.

**Résultat attendu :** un tableau de tests rempli, avec les quatre cas vérifiés.

---

## Étape 7 : documentation et discussion

**Durée : 20 min**

### Discussion à mener

- En quoi le RAG a-t-il concrètement réduit le risque d'hallucination sur vos tests ?
- Quelles sont les limites du RAG : que se passe-t-il si la FAQ est incomplète ou mal rédigée ?
- Le principe du human-in-the-loop a-t-il ralenti la réponse au client ? Comment l'équilibrer avec la rapidité attendue ?

### Modèle de fiche projet

```markdown
# Lab Service client — CRM, chatbot et RAG

## Besoin
[Résumé du scénario et de l'objectif]

## Architecture
[Site, FAQ découpée, chaîne RAG, mini CRM, écran de validation]

## FAQ utilisée
[Votre FAQ de l'étape 2]

## Tests réalisés
[Votre tableau de l'étape 6]

## Discussion RAG et human-in-the-loop
[Vos réponses ci-dessus]

## Limites identifiées
[Ce que l'application ne fait pas ou ne fait pas bien]

## Lien vers l'application déployée
[URL Replit]
```

Déployez ensuite l'application avec le bouton **Deploy** de Replit.

**Résultat attendu (livrable final du lab)** : solution déployée + architecture + jeux de tests + limites.

---

## Pousser ce lab sur GitHub

```bash
git add LAB3_SERVICE_CLIENT.md
git commit -m "Lab 3 Service client : CRM, chatbot et RAG"
git push
```

Si c'est le premier fichier du dépôt :

```bash
git init
git add LAB3_SERVICE_CLIENT.md
git commit -m "Lab 3 Service client : CRM, chatbot et RAG"
git branch -M main
git remote add origin <URL_DE_VOTRE_DEPOT>
git push -u origin main
```

---

## Aller plus loin

- Module 6 du programme : *Tester et déboguer une application IA* — utile si le chatbot se comporte mal.
- Module 7 : *Sécurité, gouvernance et déploiement* — pour approfondir l'injection de prompt, les hallucinations et la traçabilité des échanges.
