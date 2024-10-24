#1 Colocar este arquivo dentro da pasta root do projeto java
#2 Compilar aplicação
#3 ececutar comando java parar dar início a aplicação

# Cria ambiente com Maven e JDK e define referência como stage01 para uso no multi stage
FROM maven:3.8.5-openjdk-17 AS stage01

# Prepara diretório para receber projeto java
RUN mkdir -p /usr/src/app

# vincula a pasta do container como sendo a pata alvo para os comando como COPY
WORKDIR /usr/src/app

# Copia projeto para dentro da imagem
COPY ./LattesMaisMais .

# Faz o build do projeto pulando testes
#RUN mvn package -Dmaven.test.skip=true
RUN mvn package

## COMPILAÇÂO CONCLUÍDA ##

#######################################
###   SEGUNDA PARTE DO MULTISTAGE   ###
#######################################

FROM openjdk:17-jdk

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

# Copiar JAR gerado no estágio anterior usando caminho absoluto do .jar
COPY --from=stage01 /usr/src/app/target/LattesMaisMais-0.0.1-SNAPSHOT.jar app.jar

# Comando para rodar a aplicação
CMD [ "java", "-jar", "app.jar" ]

## BUILD CONMCLUÍDO ##

# Rodar comando dokcer: docker image build -t nome-imagem .
# Permitir acesso na mesma conexão host ao rodar container: docker container run --network=host nome-imagem