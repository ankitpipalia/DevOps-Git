FROM node:12-alpine

WORKDIR /backend
COPY package.json .
RUN npm install
COPY . .

EXPOSE 5000

RUN sonar-scanner

ENTRYPOINT node index.js