FROM maven:3-jdk-8 as build

COPY pom.xml pom.xml
RUN mvn -B dependency:resolve-plugins dependency:resolve
COPY src src

RUN mvn -B package

FROM java:8-jre as production

COPY --from=build /target/config.jar /app/
CMD ["java", "-Xmx200m", "-jar", "/app/config.jar"]

HEALTHCHECK --interval=30s --timeout=30s CMD curl -f http://localhost:8888/actuator/health || exit 1

EXPOSE 8888