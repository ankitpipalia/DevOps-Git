FROM node:12-alpine as build

WORKDIR /frontend
COPY . .

RUN npm i
RUN sonar-scanner -Dsonar.projectKey=Frontend   -Dsonar.sources=. -Dsonar.host.url=http://142.93.217.213:9000 -Dsonar.token=sqa_6756fbd3485096abb3f3038d95e26ab884f18041 -Dsonar.login=admin -Dsonar.password=root1234 -Dsonar.projectBaseDir=/frontend

RUN npm run-script build

FROM nginx

COPY --from=build /frontend/build /var/www/html
COPY ./default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx","-g","daemon off;"]