FROM node:14-alpine3.10

WORKDIR /app

### install your dependencies
COPY package*.json .
RUN npm ci --production

COPY ./src .

ENTRYPOINT [ "node", "/app/app.js"]
