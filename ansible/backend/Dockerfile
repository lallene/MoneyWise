# Étape 1 : Builder avec Maven
FROM maven:3.9.0-eclipse-temurin-17 AS build

WORKDIR /app

# Copier les fichiers de dépendances et builder le projet
COPY pom.xml .
RUN mvn dependency:go-offline

COPY src ./src
RUN mvn clean package -DskipTests

# Étape 2 : Runtime Java
FROM eclipse-temurin:17-jdk-alpine

WORKDIR /app

# Copier le jar généré
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080
CMD ["java", "-jar", "app.jar"]