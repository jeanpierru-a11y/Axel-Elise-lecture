# Notes de projet — Guide de Lecture · Axel & Élise

## Dernière mise à jour : 31/03/2026

---

## 🌐 Application web

| Info | Valeur |
|------|--------|
| URL live | https://jeanpierru-a11y.github.io/mon-premier-projet |
| Dépôt GitHub | github.com/jeanpierru-a11y/mon-premier-projet |
| Fichier principal | `index.html` |
| Mise à jour | Glisser `index.html` sur GitHub → Code → Add file → Upload |

---

## ✅ Fonctionnalités en place

- Bibliothèque multi-livres (ID unique, date de création, tri chronologique)
- Onglets par livre : Livre / Persos / Lieux / Temps / Mots-Citations / Intrigue / Écrire / Carnet / PDF
- Panneau NI (Nouvelle Interface) : personnages, lieux, matrice des relations, graphe D3
- Saisie vocale via micro du clavier (Android Chrome, Safari iPad, Chrome PC)
- Sauvegarde automatique en `localStorage` + sync Firebase Firestore (temps réel, offline)
- Génération PDF coloré et sobre dans le navigateur (impression Ctrl+P)
- Tri IA des notes de carnet (API Claude Sonnet) avec historique des tris
- Schéma narratif sélectionnable : Freytag 5 actes (défaut), Aristote 3 actes, Arc moderne 8 étapes
- Mode Axel (6ème) / Élise (2nde) — interface adaptée au niveau scolaire
- 5 livres démo : *Le Petit Prince*, *Tom Sawyer*, *Alice*, *Thérèse Desqueyroux*, *L'Adversaire*
- Dissertation guidée (méthode 6ème et méthode 2nde AEA)
- Analyse linéaire, commentaire littéraire, rédaction
- **Module authentification Firebase** (voir section dédiée ci-dessous)

---

## 🔐 Authentification & Contrôle d'accès

### Firebase Authentication

| Compte | E-mail | Rôle |
|--------|--------|------|
| Jean | `jean@guide-lecture.fr` | `admin` |
| Axel | `axel@guide-lecture.fr` | `eleve` |
| Élise | `elise@guide-lecture.fr` | `eleve` |
| Testeur | `testeur@guide-lecture.fr` | `testeur` |

### Règles d'accès

| Action | admin | eleve (propriétaire) | eleve (autre) | testeur |
|--------|-------|---------------------|---------------|---------|
| Lire un livre | ✅ | ✅ | ✅ | ✅ |
| Créer un livre | ✅ | ✅ | — | — |
| Modifier un livre | ✅ | ✅ | ❌ | ❌ |
| Supprimer un livre | ✅ | ✅ | ❌ | ❌ |
| Gérer les comptes | ✅ | ❌ | ❌ | ❌ |

### Propriété d'un livre

À la création, chaque livre reçoit un champ `ownerId` = UID Firebase de l'utilisateur connecté. L'admin peut lire et modifier tous les livres.

### Architecture technique

- **SDK** : `firebase-auth-compat.js` chargé dynamiquement (contrainte 4 paires `<script>`)
- **Profils** : collection Firestore `users/{uid}` avec champs `nom` (string) et `role` (string)
- **Démarrage différé** : `chargerBiblio()` n'est appelé qu'après authentification via `_apresConnexion()`
- **Contrôle côté client** : classe CSS `.ro` sur `#screen-guide` + guards `canEdit()` / `canCreate()` sur toutes les fonctions de sauvegarde
- **Contrôle côté serveur** : Firestore Security Rules

### Firestore Security Rules (publiées)

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    function isSignedIn() { return request.auth != null; }
    function uid()        { return request.auth.uid; }
    function role() {
      return get(/databases/$(database)/documents/users/$(uid())).data.role;
    }
    function isAdmin() { return role() == 'admin'; }
    function isEleve() { return role() == 'eleve'; }

    match /users/{userId} {
      allow read:  if isSignedIn() && (uid() == userId || isAdmin());
      allow write: if isSignedIn() && isAdmin();
    }

    match /familles/{familleId} {
      allow read:  if isSignedIn();
      allow write: if isSignedIn() && (isAdmin() || isEleve());
    }
  }
}
```

### Éléments masqués en lecture seule

En mode `testeur` (ou `eleve` sur un livre qui ne lui appartient pas) :
- Tous les boutons 🗑️ (supprimer) — bibliothèque et panneaux internes
- Tous les boutons 🎤 (micro)
- Tous les boutons ➕ (ajouter entité, citation, mouvement, axe…)
- Bouton ⊗ (vider notes)
- Bouton 💾 (forcer l'enregistrement)
- Bouton "+ Nouveau livre"
- Bannière orange "👁️ Lecture seule" visible dans le guide

---

## 🔧 Standards techniques

- HTML / CSS / JS pur — aucun framework
- Tout dans un seul fichier `index.html` — 5 paires `<style>`, 4 paires `<script>`
- Variables `var` dans les handlers inline (portée globale)
- Validation JS systématique avant chaque livraison (`node --check`)
- Firebase : app-compat 10.12.2, Firestore compat, Auth compat
- D3.js 7.8.5 via CDN Cloudflare
- API Claude Sonnet (Anthropic) pour le tri IA des notes

---

## 📦 Données & Versionnage

- `DEMO_VERSION` à incrémenter à chaque mise à jour des livres démo (actuel : 14)
- `localStorage['axel_biblio']` : bibliothèque locale (objet `{ livres, demoVersion, tsMaj }`)
- `localStorage['axel_mode']` : mode Axel/Élise
- Firestore : collection `familles` → document `axel-elise` (toute la BIBLIO sérialisée)
- Firestore : collection `users` → 4 documents (un par compte, ID = UID Firebase)

---

## 📋 Chantiers en attente / idées futures

| Priorité | Sujet |
|----------|-------|
| 🟡 Moyenne | Interface admin pour gérer les comptes (créer/modifier/supprimer users depuis l'app) |
| 🟡 Moyenne | Transfert de propriété d'un livre (admin uniquement) |
| 🟢 Basse | Internationalisation (FR/EN/IT/DE) — livres démo multilingues, UI multilingue |
| 🟢 Basse | Mode hors-ligne complet avec indicateur de sync |

---

## 📁 Fichiers du projet

| Fichier | Description |
|---------|-------------|
| `index.html` | Application web complète |
| `guide_le_petit_prince.txt` | Données démo Petit Prince |
| `guide_tom_sawyer.txt` | Données démo Tom Sawyer |
| `guide_alice_pays_merveilles.txt` | Données démo Alice |
| `__LE_GRIMOIRE_DU_GRAND_EXPLORATEUR_DE_RÉCITS.docx` | Guide méthodologique Word |
| `LE_GRIMOIRE_DU_GRAND_EXPLORATEUR_DE_RÉCITS.pdf` | Guide méthodologique PDF |
| `schema_narratif_fr.pdf` | Fiche schéma narratif |
| `guide_lecture_6eme_Axel.pdf` | Guide lecture 6ème |
| `therese_desqueyroux_12outils.pdf` | 12 outils Thérèse Desqueyroux |
| `adversaire_carrere_12outils.pdf` | 12 outils L'Adversaire |
| `NOTES.md` | Ce fichier |

---

## 👤 Contexte utilisateur

- **Jean** : grand-père à Fécamp (Normandie), crée et maintient l'appli — rôle `admin`
- **Axel** : 11 ans, 6ème, dyslexique — PC Windows — rôle `eleve`
- **Élise** : lycée 2nde, géographiquement éloignée — iOS/Android/iPad — rôle `eleve`
- **Testeur** : compte de démonstration en lecture seule — rôle `testeur`

---

## 🔗 Liens utiles

- Firebase Console : https://console.firebase.google.com/project/axel-elise-lecture
- GitHub Pages : https://jeanpierru-a11y.github.io/mon-premier-projet
- Anthropic Console (clé API IA) : https://console.anthropic.com
