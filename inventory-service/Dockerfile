FROM maven:3.8.4-openjdk-17-slim AS build

WORKDIR /app

COPY pom.xml .

COPY src ./src

RUN mvn clean package -DskipTests

FROM gcr.io/distroless/java17-debian12

WORKDIR /app

COPY --from=build /app/target/inventory-service-1.0.0.jar ./app.jar

EXPOSE 8081

ENTRYPOINT ["java", "-jar", "/app/app.jar"]

CMD ["--server.port=8081"]