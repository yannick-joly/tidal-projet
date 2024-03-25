# Partir de l'image officielle de PostgreSQL comme base
# https://hub.docker.com/_/postgres
FROM postgres:16
#-alpine

# Récupérer les args du build et les transmettres au conteneur
# Ils seront nécessaire à l'initialisation de la base de données.
# ARG plutôt que ENV : définies le temps du build
ARG POSTGRES_PHP_USER=${POSTGRES_PHP_USER}
ENV POSTGRES_PHP_USER=${POSTGRES_PHP_USER}

ARG POSTGRES_PHP_PASSWORD=${POSTGRES_PHP_PASSWORD}
ENV POSTGRES_PHP_PASSWORD=${POSTGRES_PHP_PASSWORD}

ARG POSTGRES_SCRIPTS_INIT_DIR=${POSTGRES_SCRIPTS_INIT_DIR}

COPY ${POSTGRES_SCRIPTS_INIT_DIR} /docker-entrypoint-initdb.d/

# Corriger les caractères de fin de ligne pour les utilisateurs de Git sous Windows
RUN apt-get update && apt-get install -y dos2unix
RUN find /docker-entrypoint-initdb.d -type f -print0 | args -0 dos2unix && \
    apt-get --purge remove -y dos2unix && \
    rm -rf /var/lib/apt/lists/*
