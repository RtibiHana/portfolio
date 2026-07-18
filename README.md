# Portfolio — Vue.js (bilingue FR/EN)

Portfolio construit avec **Vue 3 + Vite**. Design clair, bouton de bascule FR/EN en haut à droite, 8 projets affichés en grille (2 par ligne).

## 1. Lancer en local

```bash
npm install
npm run dev
```

## 2. À faire avant de publier

- **Ta photo** : remplace `public/photo.jpg` par ta vraie photo (même nom de fichier). Si le fichier est absent ou invalide, le site affiche automatiquement un avatar avec tes initiales "HR" à la place — donc rien ne casse en attendant.
- **CV anglais** : `public/cv-en.pdf` est pour l'instant une copie du CV français. Remplace-le par ta vraie version anglaise (garde le nom `cv-en.pdf`).
- **CV français** : déjà en place (`public/cv-fr.pdf`), à partir du fichier que tu as fourni.
- **Liens GitHub manquants** : dans `src/content.js`, plusieurs projets ont `repo: ''` (recrutement, DevOps, Vision-LLM, ShowGoOn, GLPI). Ajoute les URL dès que ces repos sont en ligne.
- **LinkedIn** : vérifie l'URL dans `src/App.vue` (recherche `linkedin.com/in/hana-rtibi`) et corrige si besoin.
- **Démo live** : dès qu'un projet est déployé, ajoute son URL dans le champ `demo` du projet correspondant (`src/content.js`) — le lien "Démo live" apparaîtra automatiquement.

## 3. Modifier les textes / traductions

Tout le contenu (projets, compétences, certifications, textes FR/EN) est centralisé dans **`src/content.js`**. Chaque texte a un champ `fr` et un champ `en` — pas besoin de toucher à `App.vue` pour changer le contenu.

## 4. Déployer gratuitement

1. Pousse le projet sur GitHub.
2. Va sur vercel.com ou netlify.com, connecte GitHub.
3. "New Project" → sélectionne le repo → déploie (Vite est auto-détecté).
4. Chaque `git push` redéploie automatiquement.

## 5. Structure

```
src/
  App.vue       → structure de la page + styles
  content.js     → tout le contenu bilingue (projets, skills, textes)
  style.css      → design tokens (couleurs, typographies)
public/
  cv-fr.pdf / cv-en.pdf → CV téléchargeables
  photo.jpg              → ta photo (avatar avec repli automatique si absente)
```
