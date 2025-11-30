# Stage1
FROM eclipse-temurin:17-jdk-alpine as base
WORKDIR /app
COPY . . 
RUN ./mvnw clean package -DskipTests   # or use mvn if installed

# Stage 2: Runtime (distroless or slim)
FROM gcr.io/distroless/java17
WORKDIR /app
COPY --from=base /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]




