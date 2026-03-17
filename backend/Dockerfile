# Utiliser une image Java 17 avec Maven
FROM maven:3.9.0-eclipse-temurin-17 AS build

WORKDIR /app

# Copier les fichiers du projet backend
COPY . .

# Compiler le projet
RUN mvn clean package -DskipTests

# Image finale avec Java 17
FROM eclipse-temurin:17-jdk

WORKDIR /app

# Copier le jar compilé depuis l'image build
COPY --from=build /app/target/*.jar app.jar

# Exposer le port 8080
EXPOSE 8080

# Commande pour lancer le backend
ENTRYPOINT ["java","-jar","app.jar"]
