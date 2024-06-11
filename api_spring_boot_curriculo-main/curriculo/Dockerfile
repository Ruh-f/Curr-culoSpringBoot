# Use uma imagem base do Maven para construir o aplicativo
FROM maven:3.8.5-openjdk-17 AS build

# Defina o diretório de trabalho
WORKDIR /app

# Copie o arquivo pom.xml e baixe as dependências
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copie o código fonte
COPY src ./src

# Compile e empacote a aplicação
RUN mvn clean package -DskipTests

# Use uma imagem base do Java para rodar o aplicativo
FROM openjdk:17-jdk-alpine

# Copie o jar da fase de construção para o contêiner final
COPY --from=build /app/target/*.jar app.jar

# Expor a porta que a aplicação usará
EXPOSE 8080

# Comando para executar a aplicação
ENTRYPOINT ["java","-jar","/app.jar"]
