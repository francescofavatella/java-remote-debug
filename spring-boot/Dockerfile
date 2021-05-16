FROM openjdk:8-jdk-alpine as build
WORKDIR /workspace/app
COPY gradle gradle
COPY gradlew ./
RUN ./gradlew tasks
COPY build.gradle settings.gradle ./
COPY src src
RUN ./gradlew build -x test --info


FROM openjdk:8-jdk-alpine
WORKDIR /workspace/app
COPY --from=build  /workspace/app/build/libs/*.jar spring-boot-application.jar

ENV JAVA_TOOL_OPTIONS -agentlib:jdwp=transport=dt_socket,address=5005,server=y,suspend=n

ENTRYPOINT java -jar spring-boot-application.jar