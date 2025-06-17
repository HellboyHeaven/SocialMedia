# Этап сборки
FROM node:20-alpine AS builder
WORKDIR /app

COPY package*.json ./
RUN yarn install

COPY . .
RUN yarn build

# Этап запуска
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html

# Удаляем дефолтную страницу Nginx
RUN rm /etc/nginx/conf.d/default.conf

# Добавляем минимальный конфиг для SPA
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
