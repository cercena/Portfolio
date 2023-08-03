# Use an official OpenJDK 11+ base image
FROM adoptopenjdk:11-jdk-hotspot

# Install necessary packages (PostgreSQL client for running database commands)
RUN apt-get update && apt-get install -y postgresql-client

# Set the working directory inside the container
WORKDIR /app

# Copy the application's source code and pom.xml to the working directory
COPY . .

# Run Maven to build the application and package it as a .jar file
RUN mvn clean install

# Expose the port(s) that your application is listening on
EXPOSE 8080

# Define environment variables for PostgreSQL connection
ENV DB_HOST=localhost
ENV DB_PORT=5432
ENV DB_NAME=cineclube_app
ENV DB_USER=postgres
ENV DB_PASSWORD=postgres

# Copy the built .jar file to the container
COPY ./target/cineclube-0.0.1-SNAPSHOT.jar ./app.jar

# Entry point for running the application
CMD ["java", "-jar", "app.jar"]