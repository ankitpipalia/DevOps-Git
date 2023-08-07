FROM node:12-alpine as build

WORKDIR /frontend
COPY . /frontend

RUN npm install
RUN npm sonar

RUN npm run-script build

FROM nginx

COPY --from=build /frontend/build /var/www/html
COPY ./default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx","-g","daemon off;"]