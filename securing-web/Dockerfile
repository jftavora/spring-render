#Etapa de construção
#FROM maven:3.4.3-openjdk-21 AS build
#FROM ubuntu:latest AS build

FROM maven:3.9.6-eclipse-temurin-21 AS build

#FROM openjdk:21-slim AS build
#RUN apt-get update&& apt-get-install -y maven && clean && rm-rf/var/lig/apt/lists/*

#Definir o diretório dentro do container para a aplicação
WORKDIR /app

#Copiar o pom.xml para o container
COPY securing-web/pom.xml /app/
COPY securing-web/src/ /app/src/

#Executar o Maven para compilar o projeto e gerar o JAR File
RUN mvn clean package - DskipTests

#Etapa de execução
FROM openjdk:21-slim

#Definir o diretório de trabalho para a aplicação
WORKDIR /app

#Copiar o JAR construído na etapa anterior
COPY --from=build /app/target/*.jar app.jar

#Definir a Porta que ser[a utilizada na aplicação
EXPOSE 8654

#Comando para executar a aplicação
ENTRYPOINT [ "java" , "-jar" , app.jar]