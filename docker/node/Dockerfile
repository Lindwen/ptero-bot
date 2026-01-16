FROM node:22-alpine AS builder

RUN apk add --no-cache python3 make g++

WORKDIR /app
COPY . .
RUN npm install
RUN npm run build

FROM node:22-alpine AS production

# Install Python, build tools, and OpenSSL for native modules and Prisma
RUN apk add --no-cache python3 make g++ openssl1.1-compat

WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY package*.json .
COPY prisma ./prisma
RUN npm install --production
CMD ["npm", "start"]