# Base image
FROM eclipse-temurin:21-jre

# Working directory
WORKDIR /app

# Copy files into the container
COPY target/java-ios-1.0-SNAPSHOT.jar /app/java-ios-1.0-SNAPSHOT.jar

# Entrypoint
ENTRYPOINT ["java", "-jar", "java-ios-1.0-SNAPSHOT.jar"]

# Command to run
CMD ["--help"]