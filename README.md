# 💰 TP-8 Spring Boot — Gestion de Comptes Bancaires

Une **application REST API** développée avec **Spring Boot** pour la gestion des comptes bancaires.  
Le projet permet de **créer, consulter, modifier et supprimer** des comptes, avec support des formats **JSON** et **XML**.

---
## 📋 PLAN:
1. [Description](#-description)
2. [Fonctionnalités](#-fonctionnalités)
3. [Architecture](#-architecture)
4. [Technologies Utilisées](#-technologies-utilisées)
5. [Installation](#-installation)
6. [Démarrage](#-démarrage)
7. [API Endpoints](#-api-endpoints)
8. [Exemples d'Utilisation](#-exemples-dutilisation)
9. [Configuration](#-configuration)
10. [Base de Données](#-base-de-données)
11. [Documentation Swagger](#-documentation-swagger)
12. [Tests](#-tests)
13. [Build](#-build)
14. [Auteur](#-auteur)

## 📝 Description
Ce projet est une **API RESTful** qui gère des comptes bancaires à l’aide de **Spring Boot** et **JPA/Hibernate**.  
Il expose plusieurs endpoints pour effectuer des opérations CRUD et peut retourner des données en **JSON** ou **XML**.

## ✨ Fonctionnalités
- ✅ CRUD complet sur les comptes bancaires  
- 📊 Support des formats **JSON** et **XML**  
- 🗄️ Base de données **H2** en mémoire  
- 📚 Documentation interactive **Swagger/OpenAPI**  
- 🔄 Rechargement automatique via **Spring DevTools**  
- 💾 Persistance avec **JPA/Hibernate**  

## 🏗️ Architecture

src/main/java/org/example/tp8spring/
├── 📄 Tp8SpringApplication.java          # Point d'entrée principal
├── 📁 controllers/
│   └── CompteController.java             # Endpoints REST
├── 📁 entities/
│   ├── Compte.java                       # Entité JPA Compte
│   └── TypeCompte.java                   # Enum (COURANT, EPARGNE)
└── 📁 repositories/
    └── CompteRepository.java             # Interface JPA Repository


## 🛠️ Technologies Utilisées

| Technologie | Version | Description |
|--------------|----------|-------------|
| **Spring Boot** | 3.5.7 | Framework principal |
| **Java** | 17 | Langage de programmation |
| **Maven** | 3.9.11 | Gestionnaire de dépendances |
| **H2 Database** | Runtime | Base de données en mémoire |
| **Lombok** | Latest | Réduction du code boilerplate |
| **SpringDoc OpenAPI** | 2.1.0 | Documentation Swagger |
| **Jackson XML** | Latest | Support XML |


## 💻 Installation

### Prérequis
- Java 17+
- Maven 3.6+ (ou Maven Wrapper inclus)

### Clonage du projet
```bash
git clone <votre-repo-url>
cd TP-8-spring
```
## 🚀 Démarrage
Avec Maven Wrapper
```bash
# Windows
mvnw.cmd spring-boot:run

# Linux / Mac
./mvnw spring-boot:run
```
Avec Maven installé
```bash
mvn spring-boot:run
```

## 🌐 API Endpoints


| Méthode | Endpoint        | Description               | Format   |
| ------- | --------------- | ------------------------- | -------- |
| GET     | `/comptes`      | Liste tous les comptes    | JSON/XML |
| GET     | `/comptes/{id}` | Récupère un compte par ID | JSON/XML |
| POST    | `/comptes`      | Crée un nouveau compte    | JSON/XML |
| PUT     | `/comptes/{id}` | Met à jour un compte      | JSON/XML |
| DELETE  | `/comptes/{id}` | Supprime un compte        | -        |


## 📖 Exemples d'Utilisation

### Récupérer tous les comptes (JSON)
```bash
curl -X GET http://localhost:8080/banque/comptes \
  -H "Accept: application/json"<img width="2559" height="1013" alt="Screenshot 2025-10-28 123324" src="https://github.com/user-attachments/assets/c89cbe29-e6a6-4c08-af12-066f6bcc7c4b" />

  Récupérer un compte par ID (XML)
  curl -X GET http://localhost:8080/banque/comptes/1 \
  -H "Accept: application/xml"
```
<img width="2559" height="1197" alt="Screenshot 2025-10-28 123656" src="https://github.com/user-attachments/assets/b955c723-99b4-44eb-8e48-9d484f96260a" />

### Mettre à jour un compte
```bash
curl -X PUT http://localhost:8080/banque/comptes/1 \
  -H "Content-Type: application/json" \
  -d '{
    "solde": 2000.00,
    "dateCreation": "2024-01-15",
    "type": "EPARGNE"
  }'
```
  <img width="2559" height="1273" alt="Screenshot 2025-10-28 123550" src="https://github.com/user-attachments/assets/359b0871-5bfd-4079-90df-5e988aba9a3e" />
<img width="2559" height="1221" alt="Screenshot 2025-10-28 123448" src="https://github.com/user-attachments/assets/75e37d77-2e21-401d-a0ff-9cabab79b6a7" />

### Supprimer un compte
```bash
curl -X DELETE http://localhost:8080/banque/comptes/1
```
  <img width="2559" height="1097" alt="Screenshot 2025-10-28 123733" src="https://github.com/user-attachments/assets/05be5608-8305-4cb0-91eb-9d1b619085c7" />
  
## ⚙️ Configuration


application.properties
```bash
spring.application.name=TP-8-spring
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
spring.datasource.url=jdbc:h2:mem:testdb
```


### Console H2

Accès : http://localhost:8080/h2-console

## 📊 Base de Données

Données de test créées au démarrage :
```bash
@Bean
CommandLineRunner start(CompteRepository compteRepository){
    return args -> {
        compteRepository.save(new Compte(null, Math.random()*9000, new Date(), TypeCompte.EPARGNE));
        compteRepository.save(new Compte(null, Math.random()*9000, new Date(), TypeCompte.COURANT));
        compteRepository.save(new Compte(null, Math.random()*9000, new Date(), TypeCompte.EPARGNE));
    };
```
}


## 📚 Documentation Swagger
Accessible ici :
👉 http://localhost:8080/swagger-ui.html


## 🧪 Tests
Exécuter les tests :
```bash
mvnw.cmd test
```


## 📦 Build
Générer le fichier JAR :
```bash
mvnw.cmd clean package
```


## 👨‍💻 Auteur
Ghali EL ASRI-ghaliel

