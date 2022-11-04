# Development
# --------------------
# --------------------
FROM lagden/node:latest as dev

ARG PM="npm"
ARG NODE_ENV="production"
ARG BASE="/home/node"

ENV NODE_ENV=$NODE_ENV
ENV BASE=$BASE
ENV BASE_APP=$BASE/app

RUN [[ "${PM}" != "yarn" ]] && npm i -g $PM

USER node

WORKDIR $BASE
ADD --chown=node:node . $BASE_APP

WORKDIR $BASE_APP
RUN $PM install



# Main Backend
# --------------------
# --------------------
FROM lagden/node:latest as main

ARG PM="npm"
ARG NODE_ENV="production"
ARG BASE="/home/node"

ENV NODE_ENV=$NODE_ENV
ENV BASE=$BASE
ENV BASE_APP=$BASE/app

RUN [[ "${PM}" != "yarn" ]] && npm i -g $PM

USER node

WORKDIR $BASE
ADD --chown=node:node . $BASE_APP

WORKDIR $BASE_APP
RUN bin/node/prod.js
RUN $PM install
RUN rm -rf bin/docker bin/local bin/node
RUN rm -rf .d* .e* .g* .p* .r* .y* y*



# Build Frontend
# --------------------
# --------------------
FROM lagden/node:latest as build_frontend

ARG PM="npm"
ARG NODE_ENV="production"
ARG BASE="/home/node"

ENV NODE_ENV=$NODE_ENV
ENV BASE=$BASE
ENV BASE_APP=$BASE/app

RUN [[ "${PM}" != "yarn" ]] && npm i -g $PM

USER node

WORKDIR $BASE
ADD --chown=node:node . $BASE_APP

WORKDIR $BASE_APP
RUN $PM install
RUN npm run build
RUN bin/node/prod.js



# Main Frontend
# --------------------
# --------------------
FROM lagden/node:latest as main_frontend

ARG PM="npm"
ARG NODE_ENV="production"
ARG BASE="/home/node"

ENV NODE_ENV=$NODE_ENV
ENV BASE=$BASE
ENV BASE_APP=$BASE/app

RUN [[ "${PM}" != "yarn" ]] && npm i -g $PM

USER node

WORKDIR $BASE
ADD --chown=node:node .yarn* $BASE_APP
ADD --chown=node:node *.lock $BASE_APP
COPY --from=build_frontend $BASE_APP/public $BASE_APP/public
COPY --from=build_frontend $BASE_APP/package.json $BASE_APP

WORKDIR $BASE_APP
RUN $PM install
RUN rm -rf .d* .e* .g* .p* .r* .y* y*
