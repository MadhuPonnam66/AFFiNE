FROM node:22-alpine AS builder
WORKDIR /app
COPY . .
RUN corepack enable 
RUN yarn install --frozen-lockfile
RUN yarn build

FROM node:22-alpine
WORKDIR /app
COPY --from=builder /app .
ENV NODE_ENV=production
EXPOSE 3000
CMD ["pnpm", "start"]

