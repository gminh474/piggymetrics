FROM maven:3-jdk-8 as build

COPY pom.xml pom.xml
RUN mvn -B dependency:resolve-plugins dependency:resolve
COPY src src

RUN mvn -B package

FROM openjdk:8-jre-slim as production

COPY --from=build /target/notification-service.jar /app/
CMD ["java", "-Xmx200m", "-jar", "/app/notification-service.jar"]

EXPOSE 8000