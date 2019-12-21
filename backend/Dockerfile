FROM maven:3.6.3-jdk-11 AS MAVEN_TOOL_CHAIN
COPY pom.xml /tmp/
COPY src /tmp/src/
WORKDIR /tmp/
RUN mvn package

FROM openjdk:11-oracle
VOLUME /tmp
COPY --from=MAVEN_TOOL_CHAIN /tmp/target/*.jar app.jar
ENTRYPOINT ["java", "-jar","/app.jar", "--spring.profiles.active=docker"]
