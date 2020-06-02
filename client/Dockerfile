FROM node:alpine as builder
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
RUN npm run build

FROM nginx
EXPOSE 3000

# overwrites the default configuration in order to change the default listen PORT 
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# copy all the production build assets from the builder phase
COPY --from=builder app/build /usr/share/nginx/html