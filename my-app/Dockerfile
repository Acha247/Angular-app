# Stage 1: Build the application
FROM node:18-alpine AS builder
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: serve app with nginx server
FROM nginx:alpine
COPY ./.nginx/nginx.conf /etc/nginx/nginx.conf
## Remove default nginx index page
RUN rm -rf /usr/share/nginx/html/*
COPY --from=builder /app/package.json /app/package-lock.json ./
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 3000 80
ENTRYPOINT ["nginx", "-g", "daemon off;"]
