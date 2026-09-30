# PFE

Projet de fin d'études sur la précarité alimentaire étudiante.

**Assiette Futée** (nom provisoire) est une application web qui aide les étudiants d'Île-de-France à trouver les aides alimentaires près de chez eux et à bien manger avec un petit budget.

---

## Sommaire

1. [Le projet](#1-le-projet)
2. [Cahier des charges](#2-cahier-des-charges)
3. [Organisation Git](#3-organisation-git)
4. [Workflow de travail](#4-workflow-de-travail)
5. [Conventions de commit](#5-conventions-de-commit)
6. [Règles d'équipe](#6-règles-déquipe)

---

## 1. Le projet

### Pourquoi ?

Un questionnaire mené en septembre 2026 auprès de 151 étudiants montre que :

| Constat | Chiffre |
|---|---|
| Ne connaissent aucune aide alimentaire près de chez eux | **74 %** (28 sur 38 répondants à la question) |
| Ont déjà eu recours à une aide | 18,5 % |
| Frein n°1 : manque d'infos sur les lieux et dates | 43 % |
| Frein n°2 : honte ou sentiment d'illégitimité | 39 % |
| Se disent en précarité / en présentent au moins un signe | 5 % / **26 %** |
| Dépensent moins de 200 € par mois pour manger | 63 % |
| Sautent des repas au moins un jour par mois | 50 % |

> ⚠️ Seuls 38 répondants sur 151 ont répondu à la question sur la connaissance des aides : le chiffre de 74 % est à manier avec prudence.

### Objectifs

1. **Recenser** en un seul endroit les aides alimentaires accessibles aux étudiants à Paris et en Île-de-France (lieux, horaires, conditions).
2. **Aider chaque étudiant à savoir s'il est concerné**, sans jugement, pour lever le frein de l'illégitimité.
3. **Donner des outils concrets** pour bien manger avec peu : budget, meal prep, promotions.

### Cible

Étudiants de 18 à 25 ans en Île-de-France, en particulier ceux qui vivent seuls (30 % ont un profil fragile, contre 26 % en moyenne).

| Persona | Situation | Ce qui le bloque | Ce que l'appli lui apporte |
|---|---|---|---|
| **Léa**, 20 ans, seule en studio | Budget < 100 €, saute des repas chaque semaine | Ne se sent pas « assez pauvre », ne sait pas où aller | Quiz rassurant, carte des épiceries solidaires |
| **Karim**, 22 ans, en colocation | Budget 100 à 200 €, cuisine souvent | Manque de temps et d'idées | Meal prep hebdo, liste de courses, promos |
| **Emma**, 19 ans, chez ses parents | Budget 100 à 200 €, cuisine rarement | Aucune notion du coût réel des repas | Outil budget, recettes simples, anti-gaspi |

---

## 2. Cahier des charges

### Identité visuelle

| Élément | Choix |
|---|---|
| Couleur principale | Vert sauge `#3E7C59` |
| Couleur d'accent | Abricot `#F4A259` (boutons, promos, alertes douces) |
| Fond | Crème `#FFF8EC` |
| Texte | Anthracite `#1F2937` |
| Typographies | Poppins (titres), Inter (texte) — Google Fonts |
| Illustrations | Aplats simples d'aliments, pas de photos de files d'attente |
| Ton | Tutoiement, bienveillant, sans jugement : « coup de pouce » plutôt que « aide sociale » |

Autres noms envisagés : *Frigo Plein*, *Miam Budget*, *Le Bon Platé* (disponibilité INPI et domaine .fr à vérifier).

### Pages et fonctionnalités

Chaque page renvoie vers la carte des aides quand c'est pertinent.

#### 🏠 Accueil
- Phrase d'accroche sans jugement + 3 entrées : « Est-ce que j'ai droit à un coup de pouce ? », « Trouver une aide près de chez moi », « Bien manger avec peu ».
- Champ code postal ou géolocalisation → carte filtrée.
- Bandeau « Cette semaine » : prochaines distributions et 3 bons plans.

#### ❓ Quiz « Suis-je en précarité alimentaire ? »
- 8 questions oui/non inspirées de l'échelle FIES de la FAO + 3 questions de contexte (budget, statut boursier, logement).
- Résultat en 3 niveaux : « Ça va », « Reste vigilant », « Tu as droit à un coup de pouce ».
- Aides proposées selon les réponses + lien vers l'assistante sociale du CROUS.
- **Anonyme** : aucune réponse enregistrée, tout est calculé côté client. Mention claire que ce n'est pas un diagnostic.

#### 📍 Épiceries solidaires et aides
- Carte + liste filtrables par type (épicerie solidaire, distribution gratuite, repas CROUS, anti-gaspi), ville/arrondissement, jour d'ouverture et conditions.
- Fiche par lieu : adresse, horaires, conditions, documents à apporter, prix, inscription, date de dernière vérification.
- Bloc « Comment ça se passe ? » avec témoignages d'étudiants.
- Aides financières : aide ponctuelle CROUS, bourse, APL.

#### 💰 Gérer son budget
- Calculateur : revenus − charges fixes = reste à vivre → budget nourriture conseillé par semaine et par repas.
- Suivi des dépenses de courses sur le mois, avec alerte si le rythme dépasse le budget.
- Fiches astuces : liste de courses, achat en gros, marques distributeur, congélation, restes.

#### 🍱 Meal prep *(fonctionnalité la plus demandée : 66 %)*
- Menus de la semaine générés selon le budget (20, 30, 40 €), le temps dispo, l'équipement (24 % n'ont pas de four) et le régime (halal, végétarien, allergies).
- Liste de courses automatique avec coût estimé.
- Conseils de conservation pour petits frigos.
- Astuces de la communauté, modérées.

#### 🏷️ Promotions et bons plans
- Bons plans de la semaine par enseigne proche (hard discount, marchés en fin de matinée).
- Applis anti-gaspi et réductions étudiantes.
- Comparatif de prix d'un panier type par enseigne.
- Mise à jour manuelle au début ; automatisation plus tard, sous réserve des CGU des enseignes.

---

## 3. Organisation Git

### Branches principales

| Branche | Rôle | Qui y pousse ? |
|---|---|---|
| `main` | **Projet final, stable, sans bug.** C'est la version qu'on présente. | Personne directement : uniquement via un merge de `dev` validé par l'équipe. |
| `dev` | **Branche d'intégration.** On y merge les fonctionnalités terminées pour tester la version presque finale. | Personne directement : uniquement via des Pull Requests. |

```
main  ●─────────────────────────●──────────────●   (versions stables)
       \                       /              /
dev     ●────●────●────●──────●────●────●────●     (intégration / tests)
              \    /     \   /       \  /
feature        ●──●       ●─●         ●●           (branches de travail)
```

### Nommer une branche de travail

Chaque branche part de `dev` et son nom indique **le type**, **la zone** (optionnelle), **le but** et **la personne** qui travaille dessus :

```
<type>/<zone>-<but>-<prénom>
```

- Tout en **minuscules**, mots séparés par des **tirets** `-`, **sans accents ni espaces**.
- Le but doit être court et parlant (2 à 4 mots).

**Types :**

| Type | Utilisation |
|---|---|
| `feature` | Nouvelle fonctionnalité ou nouvelle page |
| `fix` | Correction de bug |
| `style` | Design, CSS, mise en page (sans changer la logique) |
| `refactor` | Réorganisation du code sans changer le comportement |
| `docs` | Documentation (README, commentaires…) |
| `data` | Ajout ou mise à jour des données (lieux, promos, recettes…) |
| `config` | Configuration du projet, dépendances, déploiement |

**Zones (optionnelles mais recommandées) :**

| Zone | Périmètre |
|---|---|
| `front` | Interface, pages, composants |
| `back` | API, serveur, base de données |
| `full` | Touche au front et au back |

**Exemples :**

```
feature/front-quiz-precarite-jade
feature/back-api-lieux-karim
feature/front-carte-aides-lea
fix/front-filtre-arrondissement-jade
style/front-page-accueil-emma
data/back-epiceries-paris-karim
docs/readme-jade
```

---

## 4. Workflow de travail

### 1. Partir de `dev` à jour

```bash
git checkout dev
git pull origin dev
git checkout -b feature/front-quiz-precarite-jade
```

### 2. Travailler et committer régulièrement

```bash
git add .
git commit -m "feat(quiz): ajoute les 8 questions FIES"
git push -u origin feature/front-quiz-precarite-jade
```

### 3. Rester à jour avec `dev` pendant le travail

Si `dev` a bougé pendant que tu travailles :

```bash
git checkout dev
git pull origin dev
git checkout feature/front-quiz-precarite-jade
git merge dev
```

Résous les conflits éventuels **sur ta branche**, jamais sur `dev`.

### 4. Ouvrir une Pull Request vers `dev`

- Sur GitHub : **base = `dev`**, compare = ta branche.
- Décris ce que tu as fait et comment tester.
- **Au moins une autre personne** relit et approuve avant le merge.
- Une fois mergée, supprime la branche.

### 5. Mettre `main` à jour

Quand `dev` est stable et testé par l'équipe (par exemple avant un rendu ou une démo) :

- Ouvrir une Pull Request **`dev` → `main`**.
- Toute l'équipe vérifie que tout fonctionne.
- Merge, puis éventuellement un tag de version :

```bash
git checkout main
git pull origin main
git tag v1.0
git push origin v1.0
```

### Bug urgent sur `main` ?

Créer une branche `fix/...` depuis `main`, la merger dans `main` **et** dans `dev` pour ne pas perdre la correction.

---

## 5. Conventions de commit

Format :

```
<type>(<zone concernée>): <description courte au présent>
```

| Type | Exemple |
|---|---|
| `feat` | `feat(carte): ajoute le filtre par jour d'ouverture` |
| `fix` | `fix(budget): corrige le calcul du reste à vivre` |
| `style` | `style(accueil): applique les couleurs de la charte` |
| `refactor` | `refactor(quiz): découpe le calcul du score` |
| `docs` | `docs: complète le README` |
| `data` | `data(lieux): ajoute les épiceries du 13e` |
| `chore` | `chore: met à jour les dépendances` |

Un commit = une modification cohérente. Évite les `git commit -m "modifs"` 🙂

---

## 6. Règles d'équipe

- ❌ **Jamais de push direct sur `main` ni sur `dev`**, tout passe par une Pull Request.
- ✅ Toujours créer sa branche **depuis `dev` à jour**.
- ✅ Une branche = **un sujet** = **une personne** (si on est deux, on met les deux prénoms : `feature/front-carte-aides-jade-karim`).
- ✅ On teste sa branche en local **avant** d'ouvrir la PR.
- ✅ Au moins **une relecture** par un autre membre avant de merger dans `dev`.
- ✅ On supprime les branches une fois mergées.
- ✅ Pas de données personnelles ni de mots de passe dans le code (utiliser un fichier `.env`, ignoré par Git).
- 💬 En cas de doute ou de conflit compliqué : on en parle à l'équipe avant de forcer quoi que ce soit (pas de `git push --force` sur une branche partagée).

> 💡 Conseil : sur GitHub, dans *Settings → Branches*, activer une règle de protection sur `main` et `dev` (« Require a pull request before merging ») pour rendre ces règles automatiques.
