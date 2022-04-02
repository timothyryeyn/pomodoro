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
ENV PORT=3333
ENV HOST=0.0.0.0
ENV APP_KEY=8xlaZqIc72Bm_C-mQdveVtNJHsPtK0aV
ENV DRIVE_DISK=local
ENV DB_CONNECTION=mysql
ENV MYSQL_HOST=mysql
ENV MYSQL_PORT=3306
ENV MYSQL_USER=root
ENV MYSQL_PASSWORD=root
ENV MYSQL_DB_NAME=pomodoro
ENV REDIS_CONNECTION=local
ENV REDIS_HOST=redis
ENV REDIS_PORT=6379
ENV REDIS_PASSWORD=
COPY ./package*.json ./
RUN npm ci --production
COPY --from=build /home/node/app/build .
EXPOSE 3333
CMD [ "node", "server.js" ]
