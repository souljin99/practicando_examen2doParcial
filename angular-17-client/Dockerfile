FROM node:20-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npx ng build --configuration production

FROM nginx:alpine
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist/angular-17-crud /tmp/dist
RUN if [ -d /tmp/dist/browser ]; then \
      cp -r /tmp/dist/browser/. /usr/share/nginx/html/; \
    else \
      cp -r /tmp/dist/. /usr/share/nginx/html/; \
    fi
EXPOSE 80
