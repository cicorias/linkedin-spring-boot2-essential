FROM gradle:7.1.0-jdk11-openj9 as BUILDER
ARG VERSION=0.0.1-SNAPSHOT

COPY --chown=gradle:gradle . /home/gradle/src
WORKDIR /home/gradle/src
RUN gradle clean --no-daemon
RUN gradle build --no-daemon

COPY build/libs/booting-web-0.0.1-SNAPSHOT.jar build/libs/app.jar

FROM openjdk:11.0.11-jre-slim

EXPOSE 8080
RUN mkdir /app
WORKDIR /app/
COPY --from=BUILDER /home/gradle/src/build/libs/app.jar /app/app.jar

CMD java -jar app.jar
