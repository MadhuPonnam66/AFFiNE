FROM node:22-alpine AS builder
WORKDIR /app
COPY . .
RUN corepack enable 
RUN yarn install --frozen-lockfile
RUN node ./node_modules/.bin/affine build

FROM node:22-alpine
WORKDIR /app
COPY --from=builder /app/package.json ./
COPY --from=builder /app/yarn.lock ./
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/public ./public
ENV NODE_ENV=production
EXPOSE 3000
CMD ["pnpm", "start"]

