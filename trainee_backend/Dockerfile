FROM node:12-alpine

RUN mkdir /backend
COPY . /backend
WORKDIR /backend

RUN npm install
RUN npm install nodemon --global

EXPOSE 5500

ENTRYPOINT nodemon server.js && npm start