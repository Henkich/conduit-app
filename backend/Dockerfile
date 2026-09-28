# Build context: repository root (npm workspaces share one package-lock.json)
FROM node:22-alpine

WORKDIR /app
ENV NODE_ENV=production

# Manifests first: this layer is cached until dependencies change
COPY package.json package-lock.json ./
COPY backend/package.json backend/
COPY frontend/package.json frontend/
RUN npm ci --workspace backend --omit=dev && npm cache clean --force

COPY backend/ backend/

WORKDIR /app/backend
USER node
EXPOSE 3001
CMD ["node", "index.js"]
