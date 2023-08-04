# Stage 1: Build the application
FROM adoptopenjdk:11-jdk-hotspot AS builder

# Install necessary packages (PostgreSQL client for running database commands)
RUN apt-get update && apt-get install -y postgresql-client && apt-get -y install maven

# Set the working directory inside the container
WORKDIR /app

# Copy the application's source code and pom.xml to the working directory
COPY ./src ./src
COPY ./pom.xml ./pom.xml

# Run Maven to build the application and package it as a .jar file
RUN mvn clean install

# Stage 2: Create the final image
FROM adoptopenjdk:11-jre-hotspot

# Set the working directory inside the container
WORKDIR /app

# Copy the built .jar file from the previous stage to the current container
COPY --from=builder /app/target/cineclube-0.0.1-SNAPSHOT.jar ./app.jar

# Expose the port(s) that your application is listening on
EXPOSE 8081

# Define environment variables for PostgreSQL connection
ENV DB_HOST=localhost
ENV DB_PORT=5432
ENV DB_NAME=cineclube_app
ENV DB_USER=postgres
ENV DB_PASSWORD=postgres

# Entry point for running the application
CMD ["java", "-jar", "app.jar", "--server.port=8081"]
