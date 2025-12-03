# Stage1
FROM eclipse-temurin:17-jdk-alpine as build
WORKDIR /app


# Copy pom.xml first for dependency caching
COPY pom.xml .
RUN mvn -B -ntp dependency:go-offline

RUN apk add --no-cache maven
COPY . . 
RUN mvn -B -ntp clean package -DskipTests   # or use mvn if installed

# Stage 2: Runtime (distroless or slim)
FROM gcr.io/distroless/java17
WORKDIR /app
COPY --from=build /app/target/mcapp-1.0.jar /app/app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app/app.jar"]





