FROM node:14.16-alpine3.13
LABEL maintainer="lagden@gmail.com"

# Shared libraries
RUN apk add --no-cache --update libc6-compat
RUN ln -s /lib64/ld-linux-x86-64.so.2 /lib/ld-linux-x86-64.so.2

# Timezone
RUN apk add --no-cache --update tzdata
ENV TZ=America/Sao_Paulo
RUN ln -s /usr/share/zoneinfo/$TZ /etc/localtime

# Clear apk cache
RUN rm -rf /var/cache/apk/*

# Yarn 2
RUN yarn set version berry

ARG NODE_ENV="production"
ARG BASE="/home/node"

ENV NODE_ENV=$NODE_ENV
ENV BASE=$BASE
ENV BASE_APP=$BASE/app

WORKDIR $BASE
ADD --chown=node:node . $BASE_APP

USER node

WORKDIR $BASE_APP
RUN bin/prod
RUN yarn install
RUN rm -rf bin/prod .eslintrc.js .gitignore .yarnrc.yml .yarn yarn.lock
