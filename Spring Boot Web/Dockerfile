FROM maven:3.8.4-jdk-11 as builder
RUN mkdir -p /home/maven/cache_home
COPY . /home/src/java-code/
WORKDIR /home/src/java-code/
RUN mvn verify --fail-never
RUN mvn package

FROM openjdk:11-jre-slim AS pkg
EXPOSE 8080
WORKDIR /app
COPY --from=builder /home/src/java-code/target/*.jar spring-boot-application.jar

ENTRYPOINT ["java","-jar","spring-boot-application.jar"]