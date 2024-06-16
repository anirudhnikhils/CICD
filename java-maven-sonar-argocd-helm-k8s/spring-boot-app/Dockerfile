# Use AdoptOpenJDK 11 with Alpine Linux
FROM adoptopenjdk/openjdk11:alpine-jre

WORKDIR /opt/app

# Copy the JAR file from target directory into the container
COPY target/spring-boot-web.jar app.jar

# This should not be changed
ENTRYPOINT ["java","-jar","app.jar"]
