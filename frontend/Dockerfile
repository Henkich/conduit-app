# Build context: repository root (npm workspaces share one package-lock.json)

# ---- Stage 1: build static files with Vite ----
FROM node:22-alpine AS build

WORKDIR /app
COPY package.json package-lock.json ./
COPY backend/package.json backend/
COPY frontend/package.json frontend/
RUN npm ci --workspace frontend

COPY frontend/ frontend/
RUN npm run build --workspace frontend

# ---- Stage 2: serve static files with nginx ----
FROM nginx:1.29-alpine

COPY frontend/nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/frontend/dist /usr/share/nginx/html

EXPOSE 80
