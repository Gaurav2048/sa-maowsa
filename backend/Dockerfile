# -------- Stage 1: Build --------
FROM node:20-alpine AS builder

WORKDIR /app

# Install deps
COPY package*.json ./
RUN npm install

# Copy source
COPY tsconfig.json ./
COPY src ./src

# Build TS -> JS
RUN npx tsc


# -------- Stage 2: Run --------
FROM node:20-alpine

WORKDIR /app

# Only install production deps
COPY package*.json ./
RUN npm install --omit=dev

# Copy built files
COPY --from=builder /app/dist ./dist

# Expose port
EXPOSE 3000

# Run server
CMD ["node", "dist/server.js"]