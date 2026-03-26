# Notes de projet — Lecture Axel : Guide et Appli

## Dernière mise à jour : 26/03/2026

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
- 8 onglets par livre : Livre / Persos / Lieux / Temps / Mots / Avis / Dissertation / PDF
- Saisie vocale via micro du clavier (Android Chrome, Safari iPad, Chrome PC)
- Sauvegarde automatique en `localStorage` (par appareil)
- Export `.txt` et import `.txt` (synchronisation manuelle inter-appareils)
- Génération PDF coloré et sobre dans le navigateur (impression Ctrl+P)
- 3 livres démo pré-chargés au premier lancement :
  - *Le Petit Prince* — Antoine de Saint-Exupéry
  - *Les Aventures de Tom Sawyer* — Mark Twain
  - *Alice au Pays des Merveilles* — Lewis Carroll
- Dissertation guidée méthode 6ème (Intro + 2-3 arguments + Conclusion + connecteurs)
- Exemples de dissertations intégrés dans les 3 livres démo

---

## 🔧 Standards techniques

- HTML / CSS / JS pur — aucun framework
- Validation JS systématique avant chaque livraison (`node --check`)
- PDFs Python : ReportLab + DejaVu Sans, A4, marges 2cm (standard "prompt 001")
- Pas d'appel API externe dans l'appli (tout en local)

---

## 📋 Chantiers en attente

| Priorité | Sujet | Condition |
|----------|-------|-----------|
| 🟡 Moyenne | Synchronisation Firebase multi-appareils | Attente retour d'Axel après test PC |
| 🟡 Moyenne | Bouton "Voir un exemple" dans Dissertation | Attente info sur méthode du prof |
| 🟢 Basse | Amélioration PDF (mise en page avancée) | Sur demande |

---

## 📁 Fichiers du projet

| Fichier | Description |
|---------|-------------|
| `index.html` | Application web complète |
| `guide_le_petit_prince.txt` | Données démo Petit Prince |
| `guide_tom_sawyer.txt` | Données démo Tom Sawyer |
| `guide_alice_pays_merveilles.txt` | Données démo Alice |
| `guide_20000_lieues_Axel.pdf` | Guide PDF généré (20 000 Lieues) |
| `Le grimoire du grand explorateur de récits.*` | Guide méthodologique PDF + Word |
| `schema_narratif.pdf` | Fiche schéma narratif |
| `NOTES.md` | Ce fichier |

---

## 👤 Contexte utilisateur

- **Axel** : 11 ans, 6ème, dyslexique — appareil principal : **PC Windows**
- **Jean** : grand-père, crée et maintient l'appli, niveau B1-B2 anglais
- **Christèle** : autre membre de la famille suivi par Jean
