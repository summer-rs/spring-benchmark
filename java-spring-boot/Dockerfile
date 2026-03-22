# mvn builder
FROM maven:3.9-eclipse-temurin-21 AS MAVEN_BUILD
WORKDIR /build/
COPY pom.xml /build/
# build all dependencies for cache
RUN mvn dependency:go-offline -B

COPY src /build/src/
RUN mvn install -Dmaven.test.skip=true

# runner container
FROM eclipse-temurin:21-jre

WORKDIR /app

COPY --from=MAVEN_BUILD /build/target/spring-0.0.1-SNAPSHOT.jar /app/app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]