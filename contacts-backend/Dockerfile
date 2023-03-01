# FROM eclipse-temurin:11 as builder
# WORKDIR /opt/app
# COPY .mvn/ .mvn
# COPY mvnw pom.xml ./
# RUN chmod +x mvnw
# RUN ./mvnw dependency:go-offline
# COPY ./src ./src
# RUN ./mvnw clean install

# FROM openjdk:8-jdk-alpine
# VOLUME /tmp
# # ARG JAR_FILE

# COPY --from=builder ./target/contacts-backend.jar app.jar
# ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]


FROM eclipse-temurin:8 as builder
WORKDIR /opt/app
COPY .mvn/ .mvn
COPY mvnw pom.xml ./
RUN chmod +x mvnw
RUN ./mvnw dependency:go-offline
COPY ./src ./src
RUN ./mvnw clean install

FROM eclipse-temurin:8
WORKDIR /opt/app
EXPOSE 8080
COPY --from=builder /opt/app/target/*.jar /opt/app/*.jar
ENTRYPOINT ["java", "-jar", "/opt/app/*.jar" ]