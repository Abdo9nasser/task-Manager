FROM node:alpine AS builder

USER node
WORKDIR /home/node/app

COPY --chown=node:node package*.json ./
RUN npm ci --omit=dev

COPY --chown=node:node . .


FROM gcr.io/distroless/nodejs24-debian13:nonroot

WORKDIR /app

COPY --from=builder --chown=nonroot:nonroot /home/node/app .

EXPOSE 4000

CMD ["index.js"]