# 📖 Guide de Lecture — Axel & Élise

Application web de guide de lecture scolaire, hébergée sur GitHub Pages.  
Conçue par un grand-père pour accompagner deux petits-enfants dans leur lecture — Axel (6ème, dyslexie) et Élise (2nde).

🌐 **Live :** https://jeanpierru-a11y.github.io/Axel-Elise-lecture

---

## 🎯 À quoi ça sert

L'application permet à chaque élève de construire un guide de lecture complet pour chaque livre étudié : personnages, lieux, époque, mots difficiles, citations, schéma narratif, dissertation et exercices d'écriture. L'IA (Claude Sonnet) trie automatiquement les notes libres prises au fil de la lecture.

Deux modes distincts selon l'utilisateur :
- **Mode Axel (6ème)** — dissertation guidée méthode collège, vocabulaire simplifié, support dyslexie (police adaptable)
- **Mode Élise (2nde)** — outils lycée complets : analyse linéaire bac oral, commentaire littéraire bac écrit, dissertation méthode A.E.A. en 3 parties

---

## 📚 Livres démo inclus

| Livre | Auteur | Niveau |
|-------|--------|--------|
| Le Petit Prince | Antoine de Saint-Exupéry | 6ème |
| Les Aventures de Tom Sawyer | Mark Twain | 6ème |
| Alice au Pays des Merveilles | Lewis Carroll | 6ème |
| Thérèse Desqueyroux | François Mauriac | 2nde |
| L'Adversaire | Emmanuel Carrère | 2nde |

Chaque livre démo est pré-rempli avec : personnages & relations, lieux symboliques, analyse du temps narratif, 6 citations annotées, thèmes, schéma narratif complet, dissertation exemple, rédaction (récit + argumentatif), et pour les livres lycée : analyse linéaire et commentaire littéraire.

---

## ✨ Fonctionnalités

### Par livre, 9 onglets

| Onglet | Contenu |
|--------|---------|
| 📚 Livre | Titre, auteur, genre, contexte historique, courant littéraire, style |
| 👤 Perso | Fiches personnages + graphe D3 interactif des relations + matrice |
| 🗺️ Lieux | Fiches lieux avec notes symboliques |
| ⏳ Temps | Époque, ordre narratif, durée, fréquence, espace (Élise) |
| 💬 Mots | Mots difficiles + 38 procédés littéraires avec définition et exemple |
| 🎭 Intrigue | Schéma narratif au choix : Aristote (3 actes), Freytag (5 actes) ou Arc moderne (8 étapes) |
| ✍️ Écrire | Dissertation / Rédaction / Analyse linéaire / Commentaire litt. |
| 📓 Carnet | Notes libres au fil de la lecture, triées par l'IA |
| 🖨️ PDF | Export HTML/PDF coloré ou sobre |

### Onglet ✍️ Écrire — 4 sous-onglets

- **Dissertation** — méthode 6ème (Axel) ou méthode 2nde A.E.A. en 3 parties (Élise)
- **Rédaction** — récit en 5 étapes ou texte argumentatif en 4 zones
- **Analyse linéaire** *(Élise)* — introduction en 5 points, mouvements du texte, conclusion + ouverture
- **Commentaire littéraire** *(Élise)* — introduction, 3 axes développés, conclusion

### Carnet de lecture + tri IA

Saisie libre (texte ou voix) → le modèle Claude Sonnet analyse chaque note et lui attribue automatiquement une destination (personnage, lieu, temps, mots, thème, citation…), un titre court, une phase narrative, un procédé littéraire et un type de relation. L'historique de tous les tris est conservé en accordéon.

### Sync Firebase

Synchronisation transparente entre appareils via Firebase Firestore : travail hors ligne pris en charge, fusion automatique à la reconnexion. Utile pour Axel (PC) et Élise (iPad/iPhone), qui partagent les données par code famille.

---

## 🛠️ Stack technique

| Composant | Technologie |
|-----------|-------------|
| Frontend | HTML / CSS / JS pur — aucun framework |
| Graphe des relations | D3.js 7.8.5 |
| Synchronisation cloud | Firebase Firestore 10.12.2 |
| Tri IA des notes | API Anthropic — `claude-sonnet-4-20250514` |
| Hébergement | GitHub Pages |
| Persistence locale | `localStorage` |

Tout tient dans **un seul fichier `index.html`**.  
La clé API Anthropic est saisie par l'utilisateur et stockée en localStorage (jamais dans le code).

---

## 🚀 Déploiement

```
GitHub → dépôt → Add file → Upload files → glisser index.html → Commit
```

Aucune dépendance à installer, aucun build. Le fichier s'ouvre directement dans le navigateur.

---

## 📁 Fichiers du projet

| Fichier | Description |
|---------|-------------|
| `index.html` | Application complète (code + données démo) |
| `NOTES.md` | Notes de développement |
| `LE_GRIMOIRE_DU_GRAND_EXPLORATEUR_DE_RÉCITS.pdf` | Guide méthodologique imprimable (Élise) |
| `guide_lecture_6eme_Axel.pdf` | Guide méthodologique imprimable (Axel) |
| `schema_narratif_fr.pdf` | Fiche schéma narratif |
| `guide_francais_v9.pdf` | Guide méthode littérature française |
| `therese_desqueyroux_12outils.pdf` | Analyse complète Thérèse Desqueyroux (12 outils) |
| `adversaire_carrere_12outils.pdf` | Analyse complète L'Adversaire (12 outils) |
| `guide_le_petit_prince.txt` | Données démo Petit Prince |
| `guide_tom_sawyer.txt` | Données démo Tom Sawyer |
| `guide_alice_pays_merveilles.txt` | Données démo Alice |

---

## 🔢 Versionnage des données démo

La constante `DEMO_VERSION` (actuellement **12**) dans `index.html` déclenche automatiquement la mise à jour des livres démo au prochain chargement si le localStorage d'un utilisateur est plus ancien.

**Règle :** toute modification des données démo (nouveaux champs, nouveaux contenus) doit s'accompagner d'un incrément de `DEMO_VERSION`.

---

## 👥 Utilisateurs

| Utilisateur | Niveau | Appareil | Mode |
|-------------|--------|----------|------|
| Axel | 6ème — dyslexie | PC Windows | Axel |
| Élise | 2nde | iOS / Android / iPad | Élise |
| Jean | Grand-père / développeur | — | — |

---

*Généré avec Claude (Anthropic) — mars 2026*
