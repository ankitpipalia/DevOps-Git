FROM node:12-alpine

WORKDIR /backend
COPY package.json .
RUN npm i
COPY . .

EXPOSE 5000

ENTRYPOINT node index.js