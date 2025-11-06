# Etapa 1: Construcción del microservicio con Maven
FROM eclipse-temurin:17-jdk AS builder
WORKDIR /app

# Copiamos solo los archivos necesarios de este microservicio
COPY workout-service/pom.xml .
RUN apt-get update && apt-get install -y maven
RUN mvn dependency:go-offline -B

# Copiamos el código fuente del microservicio
COPY workout-service/src ./src
RUN mvn clean package -DskipTests

# Etapa 2: Imagen final
FROM eclipse-temurin:17-jdk
WORKDIR /app
COPY --from=builder /app/target/*.jar workout-service.jar

EXPOSE 8081
ENTRYPOINT ["java", "-jar", "workout-service.jar"]
