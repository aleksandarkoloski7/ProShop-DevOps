FROM node:18-alpine AS frontend-builder

WORKDIR /app/frontend

COPY frontend/package*.json ./

RUN npm install

COPY frontend/ .

RUN npm run build

FROM node:18-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install --only=production

COPY backend/ .

COPY --from=frontend-builder /app/frontend/build ./frontend/build

EXPOSE 5000

CMD ["node", "server.js"]