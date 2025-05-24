# Stage 1: Build Stage
FROM node:22-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

# Stage 2: Production Stage
FROM node:22-alpine AS production

WORKDIR /app

COPY --from=builder /app /app

EXPOSE 3000

ENV PORT=3000

CMD ["npm", "run", "start"]
