FROM node:12-alpine

WORKDIR /backend
COPY package.json .
RUN npm install
RUN npm install nodemon --global
COPY . .

EXPOSE 5500

ENTRYPOINT nodemon server.js && npm start