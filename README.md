# Plateforme de Santé Personnalisée (Healthcare Platform)

Ce projet est une plateforme de santé personnalisée développée à l'aide de microservices. Il utilise Spring Boot pour le backend, Spring Cloud Gateway pour l'API Gateway, Keycloak pour l'authentification, et Angular pour le frontend.

## Fonctionnalités principales

- **Gestion des utilisateurs** : Créez, lisez et gérez les informations des utilisateurs.
- **Authentification et autorisation** : Intégration avec Keycloak pour la gestion des utilisateurs et des rôles.
- **API Gateway** : Utilisation de Spring Cloud Gateway pour gérer les requêtes entrantes et les rediriger vers les microservices appropriés.
- **Frontend dynamique** : Application Angular pour l'interface utilisateur permettant d'interagir avec la plateforme.

## Prérequis

Avant de commencer, assurez-vous que vous avez les éléments suivants installés :

- Java 11 ou version supérieure
- Maven
- Node.js et npm
- Angular CLI
- Docker (facultatif, si vous utilisez Keycloak en tant que conteneur)

## Configuration du Backend (Spring Boot)

### 1. Cloner le projet

Clonez le projet depuis GitHub :

git clone[ https://github.com/votre-utilisateur/healthcare-platform](https://github.com/RyhabElmoncer/healthcare-platform-microservices).git
cd healthcare-platform--microservices
2. Lancer les services backend
## Le backend utilise Spring Boot avec des microservices :

Service Utilisateur : Gère la création et la récupération des utilisateurs.
API Gateway : Dirige les requêtes vers les services backend.
Lancer le service utilisateur
Naviguez dans le dossier du service utilisateur (user-service).
mvn clean install
mvn spring-boot:run
Lancer l'API Gateway
Naviguez dans le dossier de l'API Gateway (gateway-service).
Compilez et lancez le service API Gateway avec Maven :
mvn clean install
mvn spring-boot:run
3. Lancer Keycloak (facultatif)
Si vous utilisez Keycloak pour l'authentification, vous pouvez démarrer un conteneur Docker Keycloak ou installer Keycloak localement.

Démarrer Keycloak avec Docker

docker run -d -p 8080:8080 --name keycloak jboss/keycloak
Accédez à Keycloak via http://localhost:8080.

Créez un realm (par exemple : healthcare), un client (par exemple : healthcare-client), et un utilisateur.

4. Configurer l'application backend
Dans le fichier application.yml du service backend, configurez les informations de Keycloak.
keycloak:
  auth-server-url: http://localhost:8080/auth
  realm: healthcare
  resource: healthcare-client
  public-client: true
  credentials:
    secret: healthcare-secret
Frontend (Angular)
1. Installer les dépendances
Naviguez dans le dossier du frontend (frontend-angular) et installez les dépendances :
cd frontend-angular
npm install
2. Lancer l'application Angular
Démarrez l'application Angular en mode développement :
ng serve
L'application sera disponible sur http://localhost:4200.

3. Configuration de l'authentification avec Keycloak
Dans le service d'authentification (auth.service.ts), configurez l'URL de Keycloak et l'intégration avec votre frontend Angular.
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable({
  providedIn: 'root'
})
export class AuthService {

  private apiUrl = 'http://localhost:8081/api/users';  // URL du backend

  constructor(private http: HttpClient) { }

  login(email: string, password: string) {
    return this.http.post(`${this.apiUrl}/login`, { email, password });
  }
}
Tests
Les tests de chaque service peuvent être exécutés en utilisant les commandes Maven suivantes :

mvn test
Structure du projet
Le projet est organisé de la manière suivante :
healthcare-platform/
│
├── user-service/               # Service utilisateur
│   ├── src/
│   ├── pom.xml
│
├── gateway-service/            # API Gateway avec Spring Cloud Gateway
│   ├── src/
│   ├── pom.xml
│
└── frontend-angular/           # Application Angular
    ├── src/
    ├── package.json
## Technologies utilisées
Backend : Spring Boot, Spring Cloud Gateway, Keycloak
Frontend : Angular
Base de données : MySQL ou H2 pour le développement
Authentification : Keycloak
API Gateway : Spring Cloud Gateway
##Contribution
Les contributions à ce projet sont les bienvenues ! Si vous souhaitez contribuer, veuillez forker le projet, apporter vos modifications et soumettre une Pull Request.
