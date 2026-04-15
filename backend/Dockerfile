FROM node:20-alpine AS builder

WORKDIR /app

# Install build tools for native modules (better-sqlite3)
RUN apk add --no-cache python3 make g++

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

# ─── Production stage ─────────────────────────────────────
FROM node:20-alpine

WORKDIR /app

# Install runtime dependency for better-sqlite3
RUN apk add --no-cache libstdc++

COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package*.json ./

# Create data directory for SQLite
RUN mkdir -p /app/data

EXPOSE 5000

CMD ["node", "dist/server.js"]
