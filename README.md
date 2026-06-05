# ⚡ Hackathon Jury — smsmode × Code4Sud

Application de notation en temps réel pour les jurés du hackathon Code4Sud × smsmode.  
Hébergée sur GitHub Pages, synchronisée via Firebase Realtime Database.

---

## ✨ Fonctionnalités

- **Connexion par prénom** — chaque juré sélectionne son nom parmi la liste
- **Fiche équipe** — membres et sujet du projet affichés avant la notation
- **Notation pondérée** — 5 critères notés de 1 à 4 étoiles, note finale calculée sur 20
- **Sauvegarde temps réel** — chaque note est envoyée instantanément dans Firebase
- **Barre de progression** — suivi des équipes notées par le juré
- **Vue Admin protégée** — toutes les notes agrégées, moyennes et classement en direct
- **Réinitialisation** — suppression de tous les votes via la vue admin (avec confirmation)
- **100% standalone** — un seul fichier HTML, logos embarqués, aucune dépendance à installer

---

## 📊 Barème de notation

| Critère | Pondération | Description |
|---|---|---|
| Fonctionnalité du POC | 30% | Le scénario de bout en bout fonctionne-t-il ? |
| Qualité technique | 20% | Code lisible, architecture cohérente, gestion des erreurs |
| Valeur métier | 20% | Répond à un vrai besoin ? Prêt à l'intégrer ? |
| Qualité du pitch | 20% | Clarté, structure, capacité à convaincre un non-tech |
| Potentiel de réutilisabilité | 10% | README, documentation, facilité à reprendre le projet |

**Formule :** `Note finale = Σ (note_critère × pondération × 5)`

---

## 👥 Jurés & équipes

**Jurés :** Ludovic · Laurent · Guillaume · Samir · Adrien

**Équipes :** Équipe 1 à Équipe 8

---

## 🚀 Déploiement

### Prérequis

- Un compte GitHub
- Un projet Firebase avec Realtime Database activé → [console.firebase.google.com](https://console.firebase.google.com)

### Étapes

**1. Configurer Firebase**

Dans la console Firebase :
- Créer un projet → activer **Realtime Database** en mode test
- Paramètres du projet (⚙️) → Tes applications → ajouter une app Web
- Copier les valeurs de config dans `index.html` à la section `firebaseConfig`

**2. Règles de sécurité Firebase recommandées**

```json
{
  "rules": {
    "scores": {
      ".read": true,
      ".write": true
    }
  }
}
```

**3. Déployer sur GitHub Pages**

```bash
git init hackathon-jury
cd hackathon-jury
cp hackathon_notation.html index.html
cp README.md README.md
git add .
git commit -m "🚀 Initial deploy"
git push origin main
```

Dans les **Settings** du repo → **Pages** → Source : `main` / `/ (root)`

L'application est disponible en 1-2 minutes sur :
```
https://<username>.github.io/<nom-du-repo>/
```

---

## 🎯 Utilisation le jour J

| Rôle | Action |
|---|---|
| **Juré** | Ouvrir l'URL → cliquer sur son prénom → sélectionner une équipe → noter |
| **Admin** | Ouvrir l'URL → cliquer sur ★ Vue Admin → entrer le mot de passe |

### Flux de notation

```
Connexion (prénom)
  → Grille des équipes (avec statut et score si déjà notée)
    → Fiche équipe (membres + sujet)
    → Notation par critère (1 à 4 étoiles)
    → Note finale calculée automatiquement
  → Retour aux équipes → équipe suivante
```

> La note d'une équipe n'est comptabilisée dans la **moyenne admin** que lorsque le juré a rempli **tous les critères** pour cette équipe.

---

## 🏗️ Architecture

```
index.html
├── Écran de connexion      (sélection du juré)
├── Écran de choix équipe   (grille avec progression)
├── Écran de notation       (critères + fiche équipe)
├── Vue Admin               (moyennes live + classement + reset)
├── Firebase SDK (CDN)      (Realtime Database)
└── Logos embarqués         (base64 — aucun fichier externe)
```

**Structure des données Firebase :**

```json
scores/
  Ludovic/
    Équipe 1/  { poc: 3, tech: 4, value: 3, pitch: 2, reuse: 4 }
    Équipe 2/  { poc: 2, tech: 3, value: 4, pitch: 3, reuse: 2 }
  Laurent/
    ...
```

---

## 🛠️ Stack technique

| Composant | Technologie |
|---|---|
| Frontend | HTML / CSS / JavaScript vanilla |
| Sync temps réel | Firebase Realtime Database |
| Hébergement | GitHub Pages |
| Typographie | DM Sans + Space Mono (Google Fonts) |

---

## 📝 Licence

Projet interne — smsmode × Code4Sud — Hackathon juin 2026
