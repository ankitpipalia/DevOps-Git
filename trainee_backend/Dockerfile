FROM node:12-alpine

WORKDIR /backend
COPY package.json .
RUN npm install
COPY . .

EXPOSE 5000
RUN npm sonar -Dsonar.token=sqa_6756fbd3485096abb3f3038d95e26ab884f18041

ENTRYPOINT node index.js