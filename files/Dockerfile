# Base
# --------------------
# --------------------
FROM lagden/node:latest AS base

ARG PM="npm"
ARG VERSION="local"
ARG NODE_ENV="development"
ARG BASE="/home/node"

ENV VERSION=$VERSION
ENV NODE_ENV=$NODE_ENV
ENV BASE=$BASE
ENV BASE_APP=$BASE/app

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
COPY --chown=node:node package.json $BASE_APP
COPY --chown=node:node *-lock.* $BASE_APP
COPY --chown=node:node .npmrc* $BASE_APP

RUN bin/node/install
RUN rm -rf bin

CMD ["cli/run.js"]
