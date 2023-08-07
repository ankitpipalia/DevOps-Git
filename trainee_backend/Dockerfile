FROM node:12-alpine

WORKDIR /backend
COPY package.json .
RUN npm i
COPY . .

EXPOSE 5000
RUN sonar-scanner -Dsonar.projectKey=Backend   -Dsonar.sources=. -Dsonar.host.url=http://142.93.217.213:9000 -Dsonar.token=sqa_6756fbd3485096abb3f3038d95e26ab884f18041 -Dsonar.login=admin -Dsonar.password=root1234 -Dsonar.projectBaseDir=/backend

ENTRYPOINT node index.js