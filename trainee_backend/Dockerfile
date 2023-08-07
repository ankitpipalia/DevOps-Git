FROM node:12-alpine

WORKDIR /backend
COPY package.json .
RUN npm install
COPY . .

EXPOSE 5000
RUN npm sonar

ENTRYPOINT node index.js