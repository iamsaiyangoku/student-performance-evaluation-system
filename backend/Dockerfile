# === Stage 1: Build the application ===
FROM maven:3.9.6-eclipse-temurin-21 AS build
WORKDIR /app

# Copy the pom.xml and source code from the backend directory
COPY backend/pom.xml .
COPY backend/src ./src

# Build the application and skip tests to speed up deployment
RUN mvn clean package -DskipTests

# === Stage 2: Run the application ===
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app

# Copy the built JAR from the first stage
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
