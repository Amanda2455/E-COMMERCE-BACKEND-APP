# # Build
# FROM maven:3.9.6-eclipse-temurin-17 AS build
# WORKDIR /app
# COPY pom.xml .
# COPY src ./src
# RUN mvn -q -DskipTests package
#
# # Run
# FROM eclipse-temurin:17-jre
# WORKDIR /app
# COPY --from=build /app/target/*.jar app.jar
# # Keep memory small on free VMs
# ENV JAVA_TOOL_OPTIONS="-XX:+UseContainerSupport -Xms64m -Xmx256m -XX:MaxRAMPercentage=70.0"
# EXPOSE 8080
# ENTRYPOINT ["java","-jar","/app/app.jar"]

# Build
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
# Skip compiling & running tests to avoid missing test deps
RUN mvn -q -Dmaven.test.skip=true package
RUN cp target/*jar target/app.jar

# Run
FROM eclipse-temurin:17-jre
WORKDIR /app
COPY --from=build /app/target/app.jar app.jar
ENV JAVA_TOOL_OPTIONS="-Xms64m -Xmx256m"
EXPOSE 8761
ENTRYPOINT ["java","-jar","/app/app.jar"]