FROM node:21 AS builder

WORKDIR /app

COPY package*.json ./
RUN npm ci 

COPY . .
RUN npm run build

FROM node:21-alpine AS runner

WORKDIR /app

RUN npm install -g serve

# Copy just the build output, not node_modules or source
COPY --from=builder /app/dist ./dist

EXPOSE 80
CMD ["serve", "-s", "dist", "-l", "80"]
