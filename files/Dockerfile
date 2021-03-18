FROM node:14.16-alpine3.13
LABEL maintainer="lagden@gmail.com"

# Shared libraries
RUN apk add --no-cache --update libc6-compat

# Timezone
RUN apk add --no-cache --update tzdata
ENV TZ=America/Sao_Paulo
RUN ln -s /usr/share/zoneinfo/$TZ /etc/localtime

# Clear apk cache
RUN rm -rf /var/cache/apk/*

ARG NODE_ENV="production"
ARG BASE="/home/node"

ENV NODE_ENV=$NODE_ENV
ENV BASE=$BASE
ENV BASE_APP=$BASE/app

WORKDIR $BASE
ADD --chown=node:node . $BASE_APP

WORKDIR $BASE_APP
RUN npm ci --ignore-scripts --only=prod --no-audit

USER node
