# build
FROM gitlab.praktikum-services.ru:5050/std-012-042/momo-store/node:16.20.0-alpine3.17 as builder
WORKDIR /usr/src/app
COPY . .
RUN npm install
RUN npm run build

#release
FROM gitlab.praktikum-services.ru:5050/std-012-042/momo-store/nginx:stable-alpine3.17-slim
RUN sed -ri "s#(index  index.html index.htm;)#index  index.html index.htm;\n        try_files \$uri \$uri/ /index.html;#" /etc/nginx/conf.d/default.conf
COPY --from=builder /usr/src/app/dist/ /usr/share/nginx/html
EXPOSE 80