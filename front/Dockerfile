FROM node:lts as etapa01

# cria pasta no container
RUN mkdir -p /usr/src/app

# define como pasta atual
WORKDIR /usr/src/app

# copia conteúdo package<...>.json para pasta dentro da pasta app
COPY ./lattesmaismais-UI/package*.json ./

# instala dependências
RUN npm install

# copia todos os arquivos do proejto para diretório /app
COPY ./lattesmaismais-UI ./

# build criando pasta DIST
RUN npm run build

#######################################
###   SEGUNDA PARTE DO MULTISTAGE   ###
#######################################

# NGINX é um servidor HTTP
FROM nginx:alpine

# Copia pasta build do projeto JS
COPY --from=etapa01 /usr/src/app/build /usr/share/nginx/html

# Modifica configurações default do Nginx
COPY ./nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

# executar sistema - substituído por comandos em arquivo .sh
CMD [ "nginx", "-g", "daemon off;" ]