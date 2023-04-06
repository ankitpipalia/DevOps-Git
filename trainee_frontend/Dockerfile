FROM node:12-alpine

RUN mkdir /fronend
COPY . /frontend
WORKDIR /frontend

RUN npm install
RUN npm install nodemon --global

EXPOSE 3000

ENTRYPOINT nodemon server.js && npm start