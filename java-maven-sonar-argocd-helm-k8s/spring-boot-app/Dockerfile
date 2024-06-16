# Use Maven to build the application
FROM maven:3.8.1-openjdk-11 AS build

WORKDIR /app

# Copy the Maven configuration files (if any)
COPY pom.xml .

# Resolve Maven dependencies (if any)
RUN mvn dependency:go-offline

# Copy the application source code
COPY src ./src

# Build the application
RUN mvn package -DskipTests

# Use OpenJDK 11 as the base image for the runtime environment
FROM openjdk:11-jre-slim

WORKDIR /app

# Copy the packaged Spring Boot application from the build stage
COPY --from=build /app/target/your-spring-boot-app.jar ./your-spring-boot-app.jar

# Expose the port that your Spring Boot application listens on
EXPOSE 8080

# Command to run the Spring Boot application
CMD ["java", "-jar", "your-spring-boot-app.jar"]
