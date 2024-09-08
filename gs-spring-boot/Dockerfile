# Use Maven image with JDK 11
FROM maven:3.8.5-openjdk-11-slim AS build

# Set working directory
WORKDIR /app

# Copy the pom.xml and source code to the container
COPY pom.xml /app
COPY src /app/src

# Run Maven clean and package
RUN mvn clean package -DskipTests

# Second stage: Use a lightweight JRE image
FROM openjdk:11-jre-slim

# Set the working directory
WORKDIR /app

# Copy the packaged JAR from the build stage
COPY --from=build /app/target/*.jar /app/app.jar

# Expose the application port
EXPOSE 8080

# Run the application
CMD ["java", "-jar", "/app/app.jar"]
