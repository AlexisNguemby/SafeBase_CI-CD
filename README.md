SafeBase - Pipeline CI/CD

SafeBase est une application reposant sur une architecture multi-services (Backend Node.js, Frontend React et Worker Go) dotée d'un pipeline d'Intégration et de Déploiement Continus (CI/CD) automatisé via GitHub Actions.

🏗️ Architecture du Projet

Le projet se compose de 3 services principaux :

Server (/server) : API Backend développée avec Node.js.

Client (/client) : Interface utilisateur Web développée avec React.

Worker (/worker-go) : Service de traitement d'arrière-plan développé en Go.

🔄 Fonctionnement du Pipeline CI/CD

Le workflow est configuré dans .github/workflows/main.yml et se découpe en deux phases distinctes :

1. Intégration Continue (CI)

Exécutée en parallèle à chaque modification (push ou pull_request) pour valider la qualité du code source :

check-server-node : Installe les dépendances avec npm ci et lance les tests unitaires du serveur Node.js.

check-worker-go : Compile le code Go (go build) et exécute les tests unitaires.

check-client-web : Installe les dépendances et vérifie la compilation du client React (npm run build).

2. Déploiement Continu (CD)

S'exécute uniquement si les 3 étapes de CI réussissent et uniquement lors d'un push sur la branche main :

Connexion au registre de conteneurs de GitHub (GHCR).

Construction et publication des 3 images Docker suivantes :

ghcr.io/<votre-identifiant>/safebase-server:latest

ghcr.io/<votre-identifiant>/safebase-client:latest

ghcr.io/<votre-identifiant>/safebase-worker:latest

🚀 Démarrage Rapide (En local)

Prérequis

Node.js (v20+)

Go (v1.23+)

Docker

Exécution des tests localement

# Tester le serveur Node.js
cd server && npm ci && npm test

# Tester le client React
cd client && npm ci && npm run build

# Tester le worker Go
cd worker-go && go build ./... && go test ./...

