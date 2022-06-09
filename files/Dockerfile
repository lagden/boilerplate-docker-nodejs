# Development
# --------------------
# --------------------
FROM lagden/node:latest as dev

ENV NODE_ENV=$NODE_ENV
ENV BASE=$BASE
ENV BASE_APP=$BASE/app

WORKDIR $BASE
ADD --chown=node:node . $BASE_APP

USER node

WORKDIR $BASE_APP
RUN yarn set version stable
RUN yarn install



# Main Backend
# --------------------
# --------------------
FROM lagden/node:latest as main

ENV NODE_ENV=$NODE_ENV
ENV BASE=$BASE
ENV BASE_APP=$BASE/app

WORKDIR $BASE
ADD --chown=node:node . $BASE_APP

USER node

WORKDIR $BASE_APP
RUN bin/node/prod.js
RUN yarn set version stable
RUN yarn install
RUN rm -rf bin/docker bin/local bin/node
RUN rm -rf .prettierrc* .eslintrc* .git* .yarnrc* yarn.lock



# Build Frontend
# --------------------
# --------------------
FROM lagden/node:latest as build_frontend

ENV NODE_ENV=$NODE_ENV
ENV BASE=$BASE
ENV BASE_APP=$BASE/app

WORKDIR $BASE
ADD --chown=node:node . $BASE_APP

USER node

WORKDIR $BASE_APP
RUN yarn set version stable
RUN yarn install
RUN npm run build
RUN bin/node/prod.js



# Main Frontend
# --------------------
# --------------------
FROM lagden/node:latest as main_frontend

ENV NODE_ENV=$NODE_ENV
ENV BASE=$BASE
ENV BASE_APP=$BASE/app

WORKDIR $BASE
COPY --from=build_frontend $BASE_APP/public $BASE_APP/public
COPY --from=build_frontend $BASE_APP/package.json $BASE_APP
COPY --from=build_frontend $BASE_APP/yarn.lock $BASE_APP
COPY --from=build_frontend $BASE_APP/.yarnrc.yml $BASE_APP
COPY --from=build_frontend $BASE_APP/.yarn $BASE_APP

WORKDIR $BASE_APP
RUN yarn set version stable
RUN yarn install
RUN rm -rf .* yarn.lock

USER node
