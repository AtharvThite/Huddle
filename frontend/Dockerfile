# STAGE 1: Build the React App
FROM node:18 as build-stage

WORKDIR /app

# Accept build-time arguments
ARG REACT_APP_API_URL
ARG REACT_APP_SOCKET_URL

# Set them as environment variables
ENV REACT_APP_API_URL=$REACT_APP_API_URL
ENV REACT_APP_SOCKET_URL=$REACT_APP_SOCKET_URL

COPY package*.json ./
RUN npm install
COPY . .

# This command will now use the ENV vars
RUN npm run build

# STAGE 2: Serve with NGINX
FROM nginx:1.25-alpine
COPY --from=build-stage /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80