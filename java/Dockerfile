FROM maven:3.9-eclipse-temurin-21 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn package -DskipTests

FROM eclipse-temurin:21-jre
WORKDIR /app
COPY --from=build /app/target/hello-world-1.0.0.jar app.jar
EXPOSE 5001
ENTRYPOINT ["java", "-jar", "app.jar"]
