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

RUN npm install --global --ignore-scripts npm
RUN npm install --global --ignore-scripts pnpm

USER node

RUN mkdir -p $BASE_APP
WORKDIR $BASE_APP



# Development
# --------------------
# --------------------
FROM base AS dev

COPY --chown=node:node package.json $BASE_APP
COPY --chown=node:node *-lock.json $BASE_APP
COPY --chown=node:node *-lock.yaml $BASE_APP

RUN $PM install --ignore-scripts



# Main Backend
# --------------------
# --------------------
FROM base AS main

COPY --chown=node:node server $BASE_APP/server
COPY --chown=node:node package.json $BASE_APP
COPY --chown=node:node *-lock.json $BASE_APP
COPY --chown=node:node *-lock.yaml $BASE_APP

RUN $PM install --ignore-scripts

CMD ["node", "server/index.js"]



# Build Frontend
# --------------------
# --------------------
FROM base as build_frontend

COPY --chown=node:node bin $BASE_APP/bin
COPY --chown=node:node resource $BASE_APP/resource
COPY --chown=node:node src $BASE_APP/src
COPY --chown=node:node .eslintrc.cjs $BASE_APP
COPY --chown=node:node .gitignore $BASE_APP
COPY --chown=node:node .npmrc $BASE_APP
COPY --chown=node:node index.html $BASE_APP
COPY --chown=node:node package.json $BASE_APP
COPY --chown=node:node *-lock.json $BASE_APP
COPY --chown=node:node *-lock.yaml $BASE_APP
COPY --chown=node:node *.config.js $BASE_APP
COPY --chown=node:node *.config.cjs $BASE_APP
COPY --chown=node:node *.config.json $BASE_APP
COPY --chown=node:node .conf/base.sh $BASE_APP/env.sh

RUN bin/node/build



# Main Frontend
# --------------------
# --------------------
FROM lagden/httpd:sws-2.16.0 as main_frontend

ARG BASE_BUILD="/home/node/app"
EXPOSE 5001

COPY --from=build_frontend $BASE_BUILD/dist dist
CMD ["/sws", "-d", "dist", "-p", "5001", "-g", "info", "-q", "10", "-e", "false", "-c", "*"]
