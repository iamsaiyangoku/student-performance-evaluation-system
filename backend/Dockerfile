# === Stage 1: Build the JAR ===
FROM maven:3.9.6-eclipse-temurin-21 AS build
WORKDIR /app

# Copy configuration and source files
COPY backend/pom.xml .
COPY backend/src ./src

# Compile and package the executable JAR file
RUN mvn clean package -DskipTests

# === Stage 2: Runtime Environment ===
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app

# Copy the compiled JAR artifact from Stage 1
COPY --from=build /app/target/*.jar app.jar

# Expose port and run the application
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
