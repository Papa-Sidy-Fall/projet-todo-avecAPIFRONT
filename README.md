# Gestionnaire de Tâches - Application Full-Stack

Une application web moderne et complète pour gérer vos tâches avec authentification utilisateur, système de notifications automatiques, upload de médias (images et audios), et workflow automatique des tâches.

## Fonctionnalités

### Authentification & Utilisateurs
- ✅ Inscription et connexion des utilisateurs
- ✅ Gestion des sessions avec JWT
- ✅ Système de rôles et permissions

### Gestion des Tâches
- ✅ Création, modification et suppression de tâches
- ✅ Gestion des statuts : À faire → En cours → Terminé
- ✅ Assignation de tâches aux utilisateurs
- ✅ Upload d'images et enregistrements audio
- ✅ Pagination et filtrage avancé
- ✅ Statistiques des tâches par statut

### Workflow Automatique
- ✅ Changement automatique de statut après délais configurés
- ✅ Passage automatique A_FAIRE → EN_COURS (10 secondes)
- ✅ Passage automatique EN_COURS → TERMINER (30 secondes)

### Notifications
- ✅ Système de notifications en temps réel
- ✅ Notifications pour changements de statut
- ✅ Notifications pour tâches assignées
- ✅ Compteur de notifications non lues

### Interface Utilisateur
- ✅ Interface responsive et moderne avec Tailwind CSS
- ✅ Design adaptatif mobile et desktop
- ✅ Filtres : Toutes les tâches / Créées / Assignées
- ✅ Recherche et pagination

### API Backend
- ✅ API REST complète avec TypeScript
- ✅ Validation des données avec Zod
- ✅ Gestion d'erreurs robuste
- ✅ Base de données Prisma avec MySQL

## Prérequis

- Node.js (version 16 ou supérieure)
- npm ou yarn
- MySQL (serveur de base de données)

## Installation

1. **Cloner le projet** :
   ```bash
   git clone <url-du-repo>
   cd projet-todo-avecAPIFRONT
   ```

2. **Configurer le backend** :
   ```bash
   cd backend
   npm install
   ```

3. **Configurer la base de données** :
   - Créer une base de données MySQL
   - Créer un fichier `.env` dans le dossier `backend/` avec :
     ```
     DATABASE_URL="mysql://username:password@localhost:3306/database_name"
     ```
   - Générer le client Prisma :
     ```bash
     cd backend
     npx prisma generate
     ```
   - Appliquer les migrations :
     ```bash
     npx prisma migrate dev
     ```

4. **Configurer le frontend** :
   ```bash
   cd ../frontend
   npm install
   ```

## Démarrage de l'application

### Démarrage manuel

1. **Démarrer le backend** :
   ```bash
   cd backend
   npm run build
   npm start
   ```
   Le backend sera disponible sur `http://localhost:3080`

2. **Démarrer le frontend** (dans un autre terminal) :
   ```bash
   cd frontend
   npm run dev
   ```
   Le frontend sera disponible sur `http://localhost:5173`

### Démarrage automatique (Linux/Mac)

Utilisez le script `backend/start.sh` pour démarrer les deux services :
```bash
chmod +x backend/start.sh
./backend/start.sh
```

## Structure du projet

```
projet-todo-avecAPIFRONT/
├── backend/                          # API Backend Node.js/TypeScript
│   ├── prisma/
│   │   ├── schema.prisma            # Schéma base de données Prisma
│   │   └── migrations/              # Migrations de base de données
│   ├── src/
│   │   ├── controller/              # Contrôleurs API (tâches, utilisateurs, auth)
│   │   │   ├── tacheController.ts   # Gestion des tâches CRUD
│   │   │   ├── userController.ts    # Gestion des utilisateurs
│   │   │   └── AuthController.ts    # Authentification
│   │   ├── middleware/
│   │   │   ├── Auth.ts              # Middleware d'authentification JWT
│   │   │   └── uploadImage.ts       # Middleware upload de fichiers
│   │   ├── repositorie/             # Couche d'accès aux données
│   │   │   ├── tacheRepositorie.ts  # Repository des tâches
│   │   │   ├── userRepositorie.ts   # Repository des utilisateurs
│   │   │   └── IRepository.ts       # Interface générique repository
│   │   ├── route/                   # Définition des routes API
│   │   │   ├── tacheRoute.ts        # Routes des tâches
│   │   │   ├── userRoute.ts         # Routes des utilisateurs
│   │   │   └── AuthRoute.ts         # Routes d'authentification
│   │   ├── service/                 # Logique métier
│   │   │   ├── tacheService.ts      # Service des tâches
│   │   │   └── userService.ts       # Service des utilisateurs
│   │   ├── services/                # Services spécialisés
│   │   │   ├── notificationService.ts # Service de notifications
│   │   │   └── taskScheduler.ts     # Scheduler automatique des tâches
│   │   ├── types/                   # Types TypeScript
│   │   │   └── tache.ts             # Types pour les tâches
│   │   ├── utils/                   # Utilitaires
│   │   │   ├── prismclient.ts       # Client Prisma
│   │   │   └── jsonwebtoken.ts      # Utilitaires JWT
│   │   ├── validator/               # Validation des données
│   │   │   ├── tacheValidator.ts    # Validation des tâches
│   │   │   └── userValidator.ts     # Validation des utilisateurs
│   │   └── server.ts                # Point d'entrée de l'application
│   ├── uploads/                     # Fichiers uploadés (images/audio)
│   ├── package.json
│   ├── tsconfig.json
│   └── .env                         # Variables d'environnement
└── frontend/                        # Application React
    ├── public/
    │   └── vite.svg                # Assets statiques
    ├── src/
    │   ├── components/              # Composants React
    │   │   ├── TaskList.jsx         # Liste des tâches avec pagination
    │   │   ├── TaskItem.jsx         # Élément individuel de tâche
    │   │   ├── TaskForm.jsx         # Formulaire de création/modification
    │   │   ├── Login.jsx            # Formulaire de connexion
    │   │   ├── Register.jsx         # Formulaire d'inscription
    │   │   ├── NotificationBell.jsx # Cloche de notifications
    │   │   ├── TaskFilters.jsx      # Filtres de tâches
    │   │   ├── TaskStats.jsx        # Statistiques des tâches
    │   │   ├── Pagination.jsx       # Composant de pagination
    │   │   ├── AudioRecordingSection.jsx # Enregistrement audio
    │   │   ├── ImageUploadSection.jsx    # Upload d'images
    │   │   └── ...
    │   ├── contexts/
    │   │   └── AuthContext.jsx      # Contexte d'authentification
    │   ├── hooks/
    │   │   └── useAuth.js           # Hook d'authentification
    │   ├── services/
    │   │   └── api.js               # Service API pour les appels backend
    │   ├── App.jsx                  # Composant principal
    │   └── main.jsx                 # Point d'entrée React
    ├── package.json
    ├── vite.config.js
    ├── tailwind.config.js
    └── index.html
```

## Utilisation

### Démarrage rapide
1. **Inscription/Connexion** : Créez un compte ou connectez-vous via l'interface
2. **Créer une tâche** : Cliquez sur "Nouvelle tâche" et remplissez le formulaire
3. **Ajouter des médias** : Upload d'images et enregistrements audio lors de la création
4. **Gérer les tâches** : Utilisez les filtres (Toutes/Créées/Assignées) pour naviguer

### Workflow Automatique
L'application inclut un système de workflow automatique :
- **À faire** → **En cours** : Passage automatique après 10 secondes
- **En cours** → **Terminé** : Passage automatique après 30 secondes supplémentaires
- **Notifications** : Alertes automatiques lors des changements de statut

### Gestion des Notifications
- **Cloche de notifications** : Accès rapide aux notifications dans la barre supérieure
- **Types de notifications** :
  - Tâche terminée automatiquement
  - Tâche assignée
  - Changements de statut
- **Marquage comme lu** : Gestion individuelle ou marquage global

### Filtres et Recherche
- **Filtre "Toutes"** : Affiche toutes les tâches (admin)
- **Filtre "Créées"** : Tâches créées par l'utilisateur connecté
- **Filtre "Assignées"** : Tâches assignées à l'utilisateur
- **Pagination** : Navigation par pages (10 éléments par défaut)

## API Endpoints principaux

### Authentification
- `POST /auth/register` - Inscription d'un nouvel utilisateur
- `POST /auth/login` - Connexion utilisateur

### Gestion des Tâches
- `GET /taches?page=1&limit=10` - Liste paginée des tâches
- `GET /taches/:id` - Détails d'une tâche spécifique
- `POST /taches` - Créer une nouvelle tâche (avec upload image/audio)
- `PUT /taches/:id` - Modifier une tâche existante
- `DELETE /taches/:id` - Supprimer une tâche
- `PATCH /taches/:id/:status` - Changer le statut d'une tâche (A_FAIRE/EN_COURS/TERMINER)

### Gestion des Utilisateurs
- `GET /users` - Liste de tous les utilisateurs
- `GET /users/:id` - Détails d'un utilisateur spécifique

### Système de Notifications
- `GET /taches/notifications?limit=50` - Récupérer les notifications de l'utilisateur
- `PATCH /taches/notifications/:id/read` - Marquer une notification comme lue
- `PATCH /taches/notifications/read-all` - Marquer toutes les notifications comme lues
- `GET /taches/notifications/unread-count` - Compter les notifications non lues

### Upload de Fichiers
- `GET /uploads/:filename` - Accéder aux fichiers uploadés (images/audio)

## Technologies utilisées

### Backend
- **Node.js** + **Express.js** - Framework serveur
- **TypeScript** - Typage statique
- **Prisma ORM** - ORM de base de données avec MySQL
- **JWT (jsonwebtoken)** - Authentification et sessions
- **Multer** - Gestion des uploads de fichiers (images/audio)
- **Zod** - Validation des données d'entrée
- **bcrypt** - Hashage des mots de passe
- **CORS** - Gestion des requêtes cross-origin
- **Task Scheduler** - Workflow automatique des tâches

### Frontend
- **React 19** - Bibliothèque UI moderne
- **Vite** - Outil de build rapide
- **Tailwind CSS** - Framework CSS utilitaire
- **React Router DOM** - Routage côté client
- **Context API** - Gestion d'état globale
- **Fetch API** - Requêtes HTTP
- **React Audio Visualize** - Visualisation des enregistrements audio
- **ESLint** - Linting du code

### Base de données
- **MySQL** - Système de gestion de base de données
- **Prisma Migrate** - Gestion des migrations de base de données

### Outils de développement
- **TypeScript Compiler** - Compilation TypeScript
- **Vite Dev Server** - Serveur de développement frontend
- **Prisma Studio** - Interface graphique pour la base de données

## Scripts disponibles

### Backend
```bash
cd backend
npm run build          # Compiler TypeScript
npm start              # Démarrer en production
npm run dev            # Démarrer en développement (avec compilation automatique)
npx prisma studio      # Interface graphique pour explorer la base de données
npx prisma migrate dev # Appliquer les migrations en développement
npx prisma generate    # Générer le client Prisma
```

### Frontend
```bash
cd frontend
npm run dev       # Serveur de développement
npm run build     # Build de production
npm run preview   # Prévisualisation du build
npm run lint      # Linting du code
```

## Dépannage

### Problèmes courants

**Erreur de connexion à la base de données**
- Vérifiez que MySQL est démarré
- Vérifiez les identifiants dans `DATABASE_URL`
- Assurez-vous que la base de données existe

**Erreur de compilation TypeScript**
```bash
cd backend
npm run build
```

**Problème de CORS**
- Vérifiez que le frontend et le backend utilisent les bons ports
- Modifiez la configuration CORS dans `backend/src/server.ts` si nécessaire

**Uploads qui ne fonctionnent pas**
- Vérifiez que le dossier `backend/uploads/` existe et est accessible en écriture
- Vérifiez la taille des fichiers (limite par défaut)

**Notifications qui n'arrivent pas**
- Vérifiez que le scheduler est démarré (visible dans les logs du backend)
- Les tâches changent automatiquement de statut selon les délais configurés

### Logs et débogage
- **Backend** : Logs visibles dans le terminal où le serveur tourne
- **Frontend** : Ouvrez les outils de développement du navigateur (F12)
- **Base de données** : Utilisez `npx prisma studio` pour inspecter les données

## Configuration

### Variables d'environnement (fichier `.env` dans `backend/`)

```env
# Base de données
DATABASE_URL="mysql://username:password@localhost:3306/database_name"

# Port du serveur (optionnel, défaut: 3080)
PORT=3080
```

### Configuration des ports
- **Backend API** : `http://localhost:3080` (configurable via `PORT`)
- **Frontend React** : `http://localhost:5173` (Vite par défaut)

### Configuration CORS
Le backend accepte les origines suivantes par défaut :
- `http://localhost:5173` (frontend en développement)
- `http://127.0.0.1:5173`
- `http://localhost:5174`
- `http://127.0.0.1:5174`
- `http://localhost:3000`
- `http://localhost:3001`

### Upload de fichiers
- **Dossier de stockage** : `backend/uploads/`
- **Types acceptés** : Images (jpg, jpeg, png, avif, webp) et audio (wav)
- **Accès public** : Via l'endpoint `/uploads/:filename`

## Contribution

1. Fork le projet
2. Créez une branche pour votre fonctionnalité
3. Committez vos changements
4. Poussez vers la branche
5. Ouvrez une Pull Request

## Architecture et Patterns

### Backend - Architecture Hexagonale
- **Contrôleurs** : Gestion des requêtes HTTP et réponses
- **Services** : Logique métier et orchestration
- **Repositories** : Abstraction de l'accès aux données
- **Validators** : Validation des données d'entrée avec Zod
- **Middlewares** : Authentification, upload, CORS

### Frontend - Architecture Composant
- **Composants** : UI modulaire et réutilisable
- **Context** : Gestion d'état globale (authentification)
- **Hooks** : Logique réutilisable (useAuth)
- **Services** : Abstraction des appels API

### Sécurité
- **JWT** : Authentification stateless
- **bcrypt** : Hashage sécurisé des mots de passe
- **CORS** : Protection contre les requêtes cross-origin
- **Validation** : Protection contre les données malformées

## Fonctionnalités avancées

### Workflow Automatique
Le système de workflow automatique permet de simuler un processus de gestion de tâches réaliste :
- Les tâches passent automatiquement du statut "À faire" à "En cours" après 10 secondes
- Puis de "En cours" à "Terminé" après 30 secondes supplémentaires
- Idéal pour démonstration ou tests automatisés

### Système de Notifications
- Notifications temps réel pour les changements importants
- Support pour différents types d'événements
- Interface utilisateur intuitive avec compteur

### Upload Multimédia
- Support pour les images (jpg, png, avif, webp)
- Support pour l'audio (wav)
- Stockage organisé avec accès public

## Contribution

1. Fork le projet
2. Créez une branche pour votre fonctionnalité (`git checkout -b feature/nouvelle-fonctionnalite`)
3. Committez vos changements (`git commit -am 'Ajout de nouvelle fonctionnalité'`)
4. Poussez vers la branche (`git push origin feature/nouvelle-fonctionnalite`)
5. Ouvrez une Pull Request

### Standards de code
- **Backend** : TypeScript strict, ESLint
- **Frontend** : ESLint, conventions React
- **Commits** : Messages clairs en français
- **Tests** : Structure prête pour les tests (framework à définir)

## Licence

ISC - Voir le fichier LICENSE pour plus de détails