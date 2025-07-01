# Stage 1: Build
FROM gradle:8.5.0-jdk21-alpine AS build
WORKDIR /app

# Copiar todo el backend al contenedor
COPY . .

# Dar permisos al wrapper y construir (omite test y check)
RUN chmod +x ./gradlew
RUN ./gradlew clean build -x test -x check --no-daemon

# Stage 2: Run
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app

# Copiar el jar generado desde el stage build
COPY --from=build /app/build/libs/*.jar app.jar

EXPOSE 8080

# Ejecutar la app
ENTRYPOINT ["java", "-jar", "app.jar"]
