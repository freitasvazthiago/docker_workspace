# URL
ARG HOST=${HOST}

# Stage 1
FROM node:8 as react-build

COPY ./sites-available/react.conf /etc/nginx/conf.d/default.conf
# COPY --from=react-build /app/build /usr/share/nginx/html

# FILE AUTHOR / MAINTEAINER
LABEL mainteainer="THIAGO FREITAS <freitasvazthiago@gmail.com>"


# # install dependencies
# # build react-app into build/ folder

# FROM node:10-alpine AS build
# WORKDIR /usr/src/app
# RUN npm install -g yarn
# COPY package*.json ./
# RUN yarn install
# COPY . .
# ARG REACT_APP_ENVIRONMENT
# RUN yarn build

# # move build folder to nginx
# # run nginx to server static files
# FROM nginx:stable
# COPY --from=build /usr/src/app/build/ /var/www
# COPY ./deploy/nginx.conf /etc/nginx/conf.d/default.conf