# Base image
FROM node:20 AS build
WORKDIR /usr/src/app

# Copy package files and install dependencies
COPY client/package*.json ./
RUN npm install

# Copy the application files
COPY client/ ./

# Build the application
RUN npm run build

# Serve the frontend with a lightweight HTTP server
FROM nginx:alpine
COPY --from=build /usr/src/app/build /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
