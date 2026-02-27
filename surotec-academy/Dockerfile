# Etapa 1: Construcción del JAR (Build)
FROM maven:3.9.6-eclipse-temurin-21 AS build
WORKDIR /app

# Copiamos solo el pom.xml primero para descargar las dependencias (optimiza caché)
COPY pom.xml .
RUN mvn dependency:go-offline

# Copiamos el código fuente y generamos el archivo ejecutable
COPY src ./src
RUN mvn clean package -DskipTests

# Etapa 2: Ejecución del JAR (Runtime)
FROM eclipse-temurin:21-jre
WORKDIR /app

# Copiamos el archivo JAR desde la etapa de construcción
# Asegúrate de que el nombre coincida con el de tu pom.xml
COPY --from=build /app/target/surotec-academy-0.0.1-SNAPSHOT.jar app.jar

# Exponemos el puerto definido en tu application.properties
EXPOSE 8086

# Comando para iniciar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]