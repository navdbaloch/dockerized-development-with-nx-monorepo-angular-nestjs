FROM node:14-alpine As development

WORKDIR /usr/src/app

COPY package*.json ./

RUN  npm install minimist &&\
  npm install --only=development

COPY . .

RUN npm run build:api

#! this is the production image
FROM node:14-alpine as production

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

WORKDIR /usr/src

COPY package*.json ./

RUN  npm install minimist typescript ts-node lodash reflect-metadata tslib rxjs @nestjs/platform-express @types/bcrypt && \
  npm install --only=production

COPY . .
COPY --from=development /usr/src/app/dist/apps/fwa-api ./dist
EXPOSE 3333
CMD ["node", "dist/main"]
