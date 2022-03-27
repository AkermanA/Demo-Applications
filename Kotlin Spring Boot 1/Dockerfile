FROM maven:alpine-jdk11 as cache
RUN mkdir -p /home/gradle/cache_home
ENV GRADLE_USER_HOME /home/gradle/cache_home
COPY . /home/gradle/java-code/
WORKDIR /home/gradle/java-code
RUN gradle clean build -i --stacktrace

FROM gradle:5.6.4-jdk11 as builder
COPY --from=cache /home/gradle/cache_home /home/gradle/.gradle
COPY . /usr/src/java-code/
WORKDIR /usr/src/java-code
RUN gradle build -i --stacktrace

FROM openjdk:11-jre-slim AS pkg
EXPOSE 8080
WORKDIR /app
COPY --from=builder /usr/src/java-code/build/libs/*.jar spring-boot-application.jar

ENTRYPOINT ["java","-jar","spring-boot-application.jar"]