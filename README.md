# 🎮 Esports Platform

Réseau social et plateforme de recrutement dédiés à l'esport. Trois profils d'utilisateurs, **joueur**, **coach** et **manager**, y publient du contenu, présentent leurs statistiques et leur parcours, échangent par messages privés, et mettent en relation joueurs et équipes grâce à des offres de recrutement.

L'application est une **Single Page Application** en JavaScript pur (sans framework), reliée à une **API PHP** et à une base de données **SQL**.

## ✨ Fonctionnalités

### Comptes et rôles
- Inscription et connexion avec un rôle : `PLAYER`, `COACH` ou `MANAGER`
- Sessions PHP : la connexion est conservée au rechargement de la page
- Interface adaptée au rôle (par exemple, seuls les managers publient des offres)

### Fil d'actualité
- Publication de messages texte, d'images ou de vidéos
- Chargement progressif des publications (pagination)
- Le fil est consultable par les managers, sans zone de publication pour eux

### Profil
- Pseudo, biographie, avatar et bannière
- Champs propres à chaque rôle (jeu principal, région, rôle en jeu, positions, nom d'équipe)
- **Comptes de jeu** liés avec leurs statistiques : rang, taux de victoire, KDA, nombre de parties
- **Clips** de gameplay à téléverser
- **Parcours** : équipes, formations, réussites
- **Avis** sur 5 étoiles avec commentaire
- Suivi de ses propres candidatures

### Recrutement
- Les managers publient des offres (équipe, jeu, poste recherché, description)
- Les joueurs filtrent les offres et postulent avec une lettre de motivation
- Les managers consultent les candidatures et les **acceptent ou les refusent**

### Scouting
- Recherche de joueurs par nom, jeu, région et rôle
- Fiche joueur : note moyenne, jeu principal, biographie
- Actions rapides : envoyer un message, noter, signaler

### Messagerie et notifications
- Conversations privées avec compteur de messages non lus
- Notifications (messages, candidatures, avis, offres) actualisées toutes les 30 secondes
- Marquage des notifications comme lues

### Modération
- Signalement d'un utilisateur avec un motif et des détails

## 🛠️ Technologies

| Domaine | Outils |
|---|---|
| Frontend | HTML, CSS, JavaScript (SPA, `fetch`) |
| Backend | PHP (`api.php`), sessions |
| Base de données | SQL (`schema.sql`) |
| Conteneurisation | Docker |
| Déploiement | Render (`render.yaml`) |

## 🗂️ Structure du projet

```
├── index.html            # Page unique de l'application
├── style.css             # Styles de l'interface
├── script.js             # Logique frontend : navigation, appels API, rendu
├── api.php               # API backend (toutes les requêtes passent par ici)
├── schema.sql            # Schéma de la base de données
├── Dockerfile            # Image Docker
├── start.sh              # Script de démarrage
├── render.yaml           # Configuration du déploiement sur Render
└── assets/
    └── uploads/
        ├── avatars/      # Avatars (default.png par défaut)
        └── banners/      # Bannières de profil
```

## 🔌 Fonctionnement de l'API
Toutes les requêtes du frontend vont vers `api.php?action=...` :
- `GET` pour lire les données (`get_feed`, `get_profile`, `get_offers`, `get_conversations`...)
- `POST` en JSON pour les actions (`login`, `register`, `create_offer`, `send_message`...)
- `POST` en `multipart/form-data` pour les envois de fichiers (`create_post`, `upload_avatar`, `upload_clip`)

## 🚀 Installation

### Prérequis
- Git
- Docker (recommandé), ou PHP et un serveur de base de données

### Avec Docker
```bash
git clone https://github.com/Omar-Ayadi-5/gaming_platform.git
cd gaming_platform
docker build -t esports-platform .
docker run -p 8080:80 esports-platform
```
Ouvrez ensuite `http://localhost:8080`. Adaptez le port à celui défini dans le `Dockerfile`.

### Sans Docker
1. Créer la base de données et importer le schéma :
   ```bash
   mysql -u utilisateur -p nom_de_la_base < schema.sql
   ```
   Adaptez la commande si vous utilisez un autre SGBD.
2. Renseigner les identifiants de connexion à la base dans la configuration de `api.php`. Ne publiez jamais de vrais mots de passe dans le dépôt.
3. Lancer le serveur PHP :
   ```bash
   php -S localhost:8000
   ```
4. Ouvrir `http://localhost:8000`.

## ☁️ Déploiement
Le fichier `render.yaml` décrit le déploiement sur [Render](https://render.com). Les identifiants de base de données se configurent dans les variables d'environnement de Render.

## 📸 Aperçu
<!-- Ajoutez vos captures dans un dossier docs/ puis décommentez : -->
<!-- ![Fil d'actualité](docs/feed.png) -->
<!-- ![Profil](docs/profil.png) -->
<!-- ![Recrutement](docs/recrutement.png) -->

## 👥 Équipe

| Membre | Rôle |
|---|---|
| Omar Ayadi | Frontend |
| Ghassen Krimi | Frontend |
| Yomna Hlaili | Backend  |
| Maram Othmani | Backend + Database |

## 📄 Licence
Projet réalisé dans un cadre pédagogique.
