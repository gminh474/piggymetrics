FROM maven:3-jdk-8 as build

COPY pom.xml pom.xml
RUN mvn -B dependency:resolve-plugins dependency:resolve
COPY src src

RUN mvn -B package

FROM openjdk:8-jre-slim as production

COPY --from=build /target/account-service.jar /app/
CMD ["java", "-Xmx200m", "-jar", "/app/account-service.jar"]

EXPOSE 6000