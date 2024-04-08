# Use the official Maven/Java 11 image to build our application
FROM maven:3.8.4-openjdk-11-slim AS build
WORKDIR /app
COPY pom.xml .
RUN mvn -e -B dependency:resolve
COPY src src
RUN mvn -e -B package

# Use AdoptOpenJDK 11 image as the base image for the runtime environment
FROM adoptopenjdk/openjdk11:alpine-jre

# Set the working directory in the container
WORKDIR /app

# Copy the packaged JAR file from the build stage to the runtime environment
COPY --from=build /app/target/*.jar app.jar

# Expose the port that your app runs on
EXPOSE 8080

# Specify the command to run your application
CMD ["java", "-jar", "app.jar"]
