FROM node:8 AS builder

WORKDIR /home/root/

COPY admin-frontend-variables.ts conf/

RUN git clone https://github.com/lascuolaopensource/join-admin-frontend.git \
&& mv conf/admin-frontend-variables.ts join-admin-frontend/src/environments/environment.prod.ts \
&& cd join-admin-frontend \
&& npm install \
&& npx ng build -prod -aot

FROM nginx

COPY --from=builder /home/root/join-admin-frontend/dist/ /usr/share/nginx/html