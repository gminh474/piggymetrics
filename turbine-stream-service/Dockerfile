FROM maven:3-jdk-8 as build

COPY pom.xml pom.xml
RUN mvn -B dependency:resolve-plugins dependency:resolve
COPY src src

RUN mvn -B package

FROM openjdk:8-jre-slim as production

COPY --from=build /target/turbine-stream-service.jar /app/
CMD ["java", "-Xmx200m", "-jar", "/app/turbine-stream-service.jar"]

EXPOSE 8989