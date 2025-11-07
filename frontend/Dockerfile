# STAGE 1: Build the React App
FROM node:18 as build-stage

WORKDIR /app

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the source code and build the app
COPY . .
# The CI=false is from your package.json, which is good.
RUN npm run build

# STAGE 2: Serve with NGINX
FROM nginx:1.25-alpine

# Copy the static files from the build stage
COPY --from=build-stage /app/build /usr/share/nginx/html

# We need to add an NGINX config file to handle routing and proxying
# We will create this file next.
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80