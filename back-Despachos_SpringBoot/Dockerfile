# ETAPA 1: Compilación (Build)
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app

# AQUÍ EL CAMBIO: Le indicamos la subcarpeta exacta (Reemplaza el nombre si es distinto)
COPY Springboot-API-REST/pom.xml .
COPY Springboot-API-REST/src ./src

RUN mvn clean package -DskipTests

# ETAPA 2: Ejecución (Run)
FROM amazoncorretto:17-alpine
WORKDIR /app

# SEGURIDAD: Usuario sin privilegios
RUN addgroup -S despacho-group && adduser -S despacho-user -G despacho-group
USER despacho-user

COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]