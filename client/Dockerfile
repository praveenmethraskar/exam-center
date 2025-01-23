# Base Image for Client
FROM node:20 AS build-client
WORKDIR /usr/src/app

# Create a user to avoid running as root
RUN useradd -ms /bin/bash appuser
COPY client/package*.json ./
RUN npm install  # Install dependencies as root to avoid permission issues
COPY client/ ./
RUN chown -R appuser:appuser /usr/src/app  # Change ownership to appuser

USER appuser  # Switch to appuser for the rest of the process
EXPOSE 3000
CMD ["npm", "start"]

# Final Client Image
FROM node:20-slim
WORKDIR /usr/src/app
COPY --from=build-client /usr/src/app ./
EXPOSE 3000
CMD ["npm", "start"]
