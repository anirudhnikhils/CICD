# Use a suitable base image with Java 11
FROM adoptopenjdk/openjdk11:alpine-jre

# Set the working directory
WORKDIR /opt/app

# Check if the artifact (JAR file) exists
ARG artifact=target/spring-boot-web.jar

# If the artifact does not exist, run Maven build
RUN test -f ${artifact} || (apk add --no-cache maven && \
                           apk add --no-cache openjdk11 && \
                           mvn clean package)

# Copy the artifact into the container
COPY ${artifact} app.jar

# Set the entrypoint to run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
