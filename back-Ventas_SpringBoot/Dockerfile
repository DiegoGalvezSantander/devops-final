FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Cambiamos a la imagen oficial de AWS (Corretto) basada en Alpine
FROM amazoncorretto:17-alpine
WORKDIR /app

# Ajustamos la creación del usuario a la sintaxis de Alpine
RUN addgroup -S ventas-group && adduser -S ventas-user -G ventas-group
USER ventas-user

COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]