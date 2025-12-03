# Stage1
FROM eclipse-temurin:17-jdk-alpine as base
WORKDIR /app
RUN apk add --no-cache maven
COPY . . 
RUN mvn clean package -DskipTests   # or use mvn if installed

# Stage 2: Runtime (distroless or slim)
FROM gcr.io/distroless/java17
WORKDIR /app
COPY --from=base /app/target/mcapp-1.0.jar /app/app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app/app.jar"]




