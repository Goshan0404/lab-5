FROM node:20-alpine AS build

WORKDIR /app

ARG REACT_APP_API_BASE_URL

ENV REACT_APP_API_BASE_URL=$REACT_APP_API_BASE_URL

COPY package*.json ./
RUN npm install && npm cache clean --force

COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

COPY . .
RUN npm run build

FROM nginx:1.27-alpine

COPY --from=build /app/build /usr/share/nginx/html

CMD ["nginx", "-g", "daemon off;"]
