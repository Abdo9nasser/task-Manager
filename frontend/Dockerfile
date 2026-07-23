FROM node:22-alpine AS builder

USER node
WORKDIR /home/node/app

COPY --chown=node:node package*.json ./
RUN npm ci

COPY --chown=node:node . .
RUN npm run build


FROM nginxinc/nginx-unprivileged:alpine AS production

COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=builder --chown=101:101 /home/node/app/dist /usr/share/nginx/html

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]