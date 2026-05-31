FROM node:25-alpine AS build

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci --no-audit --no-fund --loglevel=verbose

COPY . .

RUN npm run build 

FROM nginx:alpine
COPY nginx.conf /ect/nginx/conf.d/default.conf

COPY --from=build /app/dist/home-ui/browser /usr/share/nginx/html
EXPOSE 80
