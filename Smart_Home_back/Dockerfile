FROM maven:3.8.4-openjdk-17 AS builder
WORKDIR /app
COPY ./src ./src
COPY ./pom.xml .
# The Spring context test requires MySQL, which starts with Compose at runtime.
RUN --mount=type=cache,target=/root/.m2 mvn -B -ntp clean package -DskipTests

# Stage 2: Create the final image
FROM  eclipse-temurin:17-jdk-alpine AS build
VOLUME /tmp
COPY --from=builder /app/target/app.jar /app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
