FROM node:24-alpine3.23

WORKDIR /app

RUN npm install figlet@1.x

COPY ./src .

ENTRYPOINT [ "node", "/app/app.js"]
