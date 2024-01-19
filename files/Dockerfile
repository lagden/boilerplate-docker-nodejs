# Base
# --------------------
# --------------------
FROM node:lts-alpine as base

ARG TZ=America/Sao_Paulo
ARG PM="npm"
ARG VERSION="local"
ARG NODE_ENV="development"
ARG BASE="/home/node"

ENV TZ=$TZ
ENV VERSION=$VERSION
ENV NODE_ENV=$NODE_ENV
ENV BASE=$BASE
ENV BASE_APP=$BASE/app

# Shared libraries
RUN apk add --no-cache --update tzdata libc6-compat libssl3 libcrypto3

# Timezone
RUN ln -s /usr/share/zoneinfo/$TZ /etc/localtime

# Clear apk cache
RUN rm -rf /var/cache/apk/*

# Install npm and pnpm
RUN npm i -g --ignore-scripts npm
RUN npm i -g --ignore-scripts pnpm

RUN node --version
RUN npm --version
RUN pnpm --version

USER node

RUN mkdir -p $BASE_APP
WORKDIR $BASE_APP



# Development
# --------------------
# --------------------
FROM base AS dev

COPY --chown=node:node package.json $BASE_APP
RUN bin/node/install



# Main Backend
# --------------------
# --------------------
FROM base AS main

COPY --chown=node:node bin $BASE_APP/bin
COPY --chown=node:node cli $BASE_APP/cli
COPY --chown=node:node server $BASE_APP/server
# COPY --chown=node:node dist $BASE_APP/dist
# COPY --chown=node:node public $BASE_APP/public
COPY --chown=node:node package.json $BASE_APP
COPY --chown=node:node *-lock.* $BASE_APP
COPY --chown=node:node *.lock $BASE_APP
COPY --chown=node:node .npmrc* $BASE_APP

RUN bin/node/install
RUN rm -rf bin

CMD ["cli/run.js"]
