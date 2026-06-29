FROM maven:3.9.9-eclipse-temurin-17 AS build
WORKDIR /app

COPY pom.xml ./
RUN mvn -q -DskipTests dependency:go-offline

COPY src src
RUN mvn -q -DskipTests package

FROM eclipse-temurin:17-jre-jammy AS runtime
WORKDIR /app

RUN useradd --create-home --uid 10001 appuser

COPY --from=build /app/target/*.jar /app/app.jar

EXPOSE 8081
USER appuser

ENTRYPOINT ["java", "-jar", "/app/app.jar"]