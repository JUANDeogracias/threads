# Fase de construcción
FROM maven:3.8.8-eclipse-temurin-17 AS build

# Establecer el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copiar el archivo pom.xml para descargar las dependencias
COPY pom.xml .

# Descargar dependencias
RUN mvn dependency:go-offline -B

# Copiar el código fuente
COPY src ./src

# Compilar la aplicación
RUN mvn clean package

# Fase de ejecución
FROM eclipse-temurin:17-jdk-jammy

# Establecer el directorio de trabajo en el contenedor
WORKDIR /app

# Copiar el JAR compilado desde la fase de construcción
COPY --from=build /app/target/*.jar app.jar

# Exponer el puerto (ajusta según sea necesario)
EXPOSE 8080

# Comando para ejecutar la aplicación
CMD ["java", "-jar", "app.jar"]
