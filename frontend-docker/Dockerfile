FROM node:8 AS builder

WORKDIR /home/root/

COPY frontend-variables.ts conf/

RUN git clone https://github.com/lascuolaopensource/join-frontend.git \
&& mv conf/frontend-variables.ts join-frontend/src/environments/environment.prod.ts \
&& cd join-frontend \
&& npm install \
&& npx ng build -prod -aot

FROM nginx

COPY --from=builder /home/root/join-frontend/dist/ /usr/share/nginx/html