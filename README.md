# ⚡ Hackathon Jury — smsmode × Code4Sud

Application de notation en temps réel pour les jurés du hackathon, hébergée sur GitHub Pages et synchronisée via Firebase Realtime Database.

---

## ✨ Fonctionnalités

- **Connexion par prénom** — chaque juré sélectionne son nom (Ludovic, Laurent, Guillaume, Samir, Adrien)
- **Notation pondérée** — 5 critères notés de 1 à 4, avec pondération automatique pour une note finale sur 20
- **Sauvegarde temps réel** — chaque note est envoyée instantanément dans Firebase
- **Barre de progression** — suivi visuel des équipes notées par le juré
- **Vue Admin live** — toutes les notes agrégées, moyennes par équipe, classement en direct
- **100% standalone** — un seul fichier HTML, aucune dépendance à installer

---

## 📊 Barème de notation

| Critère | Pondération | Description |
|---|---|---|
| Fonctionnalité du POC | 30% | Le scénario de bout en bout fonctionne-t-il ? |
| Qualité technique | 20% | Code lisible, architecture cohérente, gestion des erreurs |
| Valeur métier | 20% | Répond à un vrai besoin ? Prêt à l'intégrer ? |
| Qualité du pitch | 20% | Clarté, structure, capacité à convaincre un non-tech |
| Potentiel de réutilisabilité | 10% | README, documentation, facilité à reprendre le projet |

**Formule :** `Note finale = Σ (note_critère / 4 × pondération × 20)`

---

## 🚀 Déploiement

### Prérequis

- Un compte GitHub
- Un projet Firebase avec Realtime Database activé ([console.firebase.google.com](https://console.firebase.google.com))

### Étapes

**1. Configurer Firebase**

Dans la console Firebase :
- Créer un projet → activer **Realtime Database** en mode test
- Paramètres du projet → Tes applications → ajouter une app Web
- Copier la config générée dans `index.html` (section `firebaseConfig`)

**2. Déployer sur GitHub Pages**

```bash
# Cloner ou créer le repo
git init hackathon-jury
cd hackathon-jury

# Copier le fichier (renommé en index.html)
cp hackathon_notation.html index.html

# Pousser sur GitHub
git add index.html README.md
git commit -m "🚀 Initial deploy"
git push origin main
```

Puis dans les **Settings** du repo → **Pages** → Source : `main` / `/ (root)`

L'application est disponible en 1-2 minutes sur :
```
https://<ton-username>.github.io/<nom-du-repo>/
```

---

## 👥 Utilisation le jour J

| Rôle | Action |
|---|---|
| **Juré** | Ouvrir l'URL → cliquer sur son prénom → noter chaque équipe |
| **Admin** | Ouvrir l'URL → cliquer sur ★ Vue Admin → suivre les notes en live |

### Flux de notation

```
Connexion → Sélection de l'équipe → Note 1 à 4 étoiles par critère
         → Sauvegarde automatique → Passer à l'équipe suivante
```

La note d'une équipe n'est comptabilisée dans la moyenne admin que lorsque le juré a **rempli tous les critères** pour cette équipe.

---

## 🏗️ Architecture

```
index.html
├── Interface juré        (notation par équipe et critère)
├── Interface admin       (vue agrégée temps réel)
├── Firebase SDK (CDN)    (sync Realtime Database)
└── Logos embarqués       (base64 — aucun fichier externe)
```

Les données sont stockées dans Firebase selon cette structure :

```json
scores/
  Ludovic/
    Équipe 1/
      poc: 3
      tech: 4
      value: 3
      pitch: 2
      reuse: 4
    Équipe 2/
      ...
  Laurent/
    ...
```

---

## 🛠️ Stack technique

- HTML / CSS / JavaScript vanilla
- [Firebase Realtime Database](https://firebase.google.com/docs/database) — sync temps réel
- [Google Fonts](https://fonts.google.com) — DM Sans + Space Mono
- GitHub Pages — hébergement statique gratuit

---

## 📝 Licence

Projet interne — smsmode × Code4Sud — Hackathon 2025
