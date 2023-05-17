# Development
# --------------------
# --------------------
FROM lagden/node:latest as dev

ARG PM="npm"
ARG NODE_ENV="development"
ARG BASE="/home/node"

ENV NODE_ENV=$NODE_ENV
ENV BASE=$BASE
ENV BASE_APP=$BASE/app

RUN [[ "${PM}" == "yarn" ]] && echo "via ${PM}" || npm i -g $PM

USER node

RUN mkdir -p $BASE_APP
WORKDIR $BASE_APP

COPY --chown=node:node . $BASE_APP
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

RUN [[ "${PM}" == "yarn" ]] && echo "via ${PM}" || npm i -g $PM

USER node

RUN mkdir -p $BASE_APP
WORKDIR $BASE_APP

COPY --chown=node:node . $BASE_APP
RUN [[ "${PM}" == "yarn" ]] && yarn plugin import workspace-tools;yarn workspaces focus --all --production || $PM i
RUN rm -rf bin/docker bin/local bin/node
RUN rm -rf .d* .e* .g* .p* .r* .y* *.lock



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

RUN [[ "${PM}" == "yarn" ]] && echo "via ${PM}" || npm i -g $PM

USER node

RUN mkdir -p $BASE_APP
WORKDIR $BASE_APP

COPY --chown=node:node . $BASE_APP

RUN [[ "${PM}" == "yarn" ]] && $PM install || echo "via ${PM}"
RUN [[ "${PM}" == "pnpm" ]] && $PM i --prod --dev || echo "via ${PM}"
RUN [[ "${PM}" == "npm" ]] && $PM i --production=false || echo "via ${PM}"

RUN npm run build



# Main Frontend
# --------------------
# --------------------
FROM lagden/httpd:sws-2.16.0 as main_frontend

ARG BASE="/"
ARG BASE_BUILD="/home/node/app"

WORKDIR $BASE
COPY --from=build_frontend $BASE_BUILD/dist*/ dist
