FROM node:12-alpine as build

RUN mkdir /fronend
COPY . /frontend
WORKDIR /frontend

RUN npm install
RUN npm install nodemon --global

EXPOSE 3000

RUN npm run-script build

FROM nginx

COPY --from=build /frontend/build /var/www/html
COPY --from=build /frontend/default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx","-g","daemon off;"]