ARG NODE_IMAGE=node:16.13.1-alpine

FROM $NODE_IMAGE AS base
RUN mkdir -p /home/node/app
WORKDIR /home/node/app
RUN mkdir tmp

FROM base AS dependencies
COPY ./package*.json ./
RUN npm ci
COPY . .

FROM dependencies AS build
RUN npm run build

FROM base AS production
ENV NODE_ENV=production
COPY ./package*.json ./
RUN npm ci --production
COPY --from=build /home/node/app/build .
EXPOSE 3333
CMD [ "node", "server.js" ]
