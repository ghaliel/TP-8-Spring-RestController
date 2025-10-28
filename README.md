
<div align="center">

![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.7-brightgreen.svg)
![Java](https://img.shields.io/badge/Java-17-orange.svg)
![Maven](https://img.shields.io/badge/Maven-3.9.11-blue.svg)
![H2 Database](https://img.shields.io/badge/H2-Database-blue.svg)
![Swagger](https://img.shields.io/badge/Swagger-OpenAPI-green.svg)

</div>

## 📋 Table des Matières

- Description
- Fonctionnalités
- Architecture
- Technologies Utilisées
- Installation
- Démarrage
- API Endpoints
- Exemples d'Utilisation
- Configuration
- Base de Données

---

## 📝 Description

Application REST API développée avec **Spring Boot** pour la gestion de comptes bancaires. Le projet permet de créer, consulter, modifier et supprimer des comptes avec support des formats **JSON** et **XML**.

---

## ✨ Fonctionnalités

- ✅ **CRUD complet** sur les comptes bancaires
- 📊 Support **JSON** et **XML**
- 🗄️ Base de données **H2** en mémoire
- 📚 Documentation **Swagger/OpenAPI**
- 🔄 Rechargement automatique avec **DevTools**
- 💾 Persistance JPA/Hibernate
- 🎯 Architecture REST propre

---

## 🏗️ Architecture

```
src/main/java/org/example/tp8spring/
├── 📄 Tp8SpringApplication.java          # Point d'entrée principal
├── 📁 controllers/
│   └── CompteController.java             # Endpoints REST
├── 📁 entities/
│   ├── Compte.java                       # Entité JPA Compte
│   └── TypeCompte.java                   # Enum (COURANT, EPARGNE)
└── 📁 repositories/
    └── CompteRepository.java             # Interface JPA Repository
```

### Modèle de Données

**Compte** :
- `id` : Long (auto-généré)
- `solde` : double
- `dateCreation` : Date
- `type` : TypeCompte (COURANT | EPARGNE)

---

## 🛠️ Technologies Utilisées

| Technologie | Version | Description |
|------------|---------|-------------|
| Spring Boot | 3.5.7 | Framework principal |
| Java | 17 | Langage de programmation |
| Maven | 3.9.11 | Gestionnaire de dépendances |
| H2 Database | Runtime | Base de données en mémoire |
| Lombok | Latest | Réduction du code boilerplate |
| SpringDoc OpenAPI | 2.1.0 | Documentation Swagger |
| Jackson XML | Latest | Support XML |

---

## 💻 Installation

### Prérequis

- **Java 17** ou supérieur
- **Maven 3.6+** (ou utiliser le wrapper inclus)

### Cloner le projet

```bash
git clone <votre-repo-url>
cd TP-8-spring
```

---

## 🚀 Démarrage

### Avec Maven Wrapper (recommandé)

**Windows :**
```bash
mvnw.cmd spring-boot:run
```

**Linux/Mac :**
```bash
./mvnw spring-boot:run
```

### Avec Maven installé

```bash
mvn spring-boot:run
```

L'application démarre sur **http://localhost:8080**

---

## 🌐 API Endpoints

### Base URL
```
http://localhost:8080/banque
```

### Endpoints Disponibles

| Méthode | Endpoint | Description | Format |
|---------|----------|-------------|--------|
| `GET` | `/comptes` | Liste tous les comptes | JSON/XML |
| `GET` | `/comptes/{id}` | Récupère un compte par ID | JSON/XML |
| `POST` | `/comptes` | Crée un nouveau compte | JSON/XML |
| `PUT` | `/comptes/{id}` | Met à jour un compte | JSON/XML |
| `DELETE` | `/comptes/{id}` | Supprime un compte | - |

---

## 📖 Exemples d'Utilisation




![img_4.png](img_4.png)
![img_5.png](img_5.png)
### 1️⃣ Récupérer tous les comptes (JSON)

```bash
curl -X GET http://localhost:8080/banque/comptes \
  -H "Accept: application/json"
```

**Réponse :**
```json
[
  {
    "id": 1,
    "solde": 5432.21,
    "dateCreation": "2024-01-15",
    "type": "EPARGNE"
  },
  {
    "id": 2,
    "solde": 7890.45,
    "dateCreation": "2024-01-15",
    "type": "COURANT"
  }
]
```


### 2️⃣ Récupérer un compte par ID (XML)

```bash
curl -X GET http://localhost:8080/banque/comptes/1 \
  -H "Accept: application/xml"
```

**Réponse :**
```xml
<Compte>
  <id>1</id>
  <solde>5432.21</solde>
  <dateCreation>2024-01-15</dateCreation>
  <type>EPARGNE</type>
</Compte>
```

### 3️⃣ Créer un nouveau compte (JSON)

```bash
curl -X POST http://localhost:8080/banque/comptes \
  -H "Content-Type: application/json" \
  -d '{
    "solde": 1000.00,
    "dateCreation": "2024-01-15",
    "type": "COURANT"
  }'
```
![img_2.png](img_2.png)
![img_3.png](img_3.png)
### 4️⃣ Mettre à jour un compte (JSON)

```bash
curl -X PUT http://localhost:8080/banque/comptes/1 \
  -H "Content-Type: application/json" \
  -d '{
    "solde": 2000.00,
    "dateCreation": "2024-01-15",
    "type": "EPARGNE"
  }'
```
![img.png](img.png)
### 5️⃣ Supprimer un compte

```bash
curl -X DELETE http://localhost:8080/banque/comptes/1
```
![img_1.png](img_1.png)
---

## ⚙️ Configuration

### Fichier application.properties

```properties
# Nom de l'application
spring.application.name=TP-8-spring

# Configuration H2 (optionnelle)
# spring.h2.console.enabled=true
# spring.datasource.url=jdbc:h2:mem:testdb
```

### Accès à la console H2

Pour activer la console H2, ajoutez dans `application.properties` :

```properties
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
```

Accès : **http://localhost:8080/h2-console**

---

## 📊 Base de Données

### Données de Test

Au démarrage, 3 comptes sont automatiquement créés via `Tp8SpringApplication` :

```java
@Bean
CommandLineRunner start(CompteRepository compteRepository){
    return args -> {
        compteRepository.save(new Compte(null, Math.random()*9000, new Date(), TypeCompte.EPARGNE));
        compteRepository.save(new Compte(null, Math.random()*9000, new Date(), TypeCompte.COURANT));
        compteRepository.save(new Compte(null, Math.random()*9000, new Date(), TypeCompte.EPARGNE));
    };
}
```

---

## 📚 Documentation Swagger

Accès à la documentation interactive de l'API :

```
http://localhost:8080/swagger-ui.html
```

---

## 🧪 Tests

Lancer les tests :

```bash
mvnw.cmd test
```

---

## 📦 Build

Créer un fichier JAR :

```bash
mvnw.cmd clean package
```

Le JAR sera généré dans `target/TP-8-spring-0.0.1-SNAPSHOT.jar`

---

## 🤝 Contribution

Les contributions sont les bienvenues ! N'hésitez pas à ouvrir une issue ou une pull request.

---

## 📄 Licence

Ce projet est à usage éducatif.

---

## 👨‍💻 Auteur

Projet développé dans le cadre du TP-8-Spring

---

<div align="center">
  <p>Fait avec ❤️ avec Spring Boot</p>
</div>