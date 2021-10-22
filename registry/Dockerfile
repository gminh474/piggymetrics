FROM maven:3-jdk-8 as build

COPY pom.xml pom.xml
RUN mvn -B dependency:resolve-plugins dependency:resolve
COPY src src

RUN mvn -B package

FROM openjdk:8-jre-slim as production

COPY --from=build /target/registry.jar /app/
CMD ["java", "-Xmx200m", "-jar", "/app/registry.jar"]

EXPOSE 8761