# Base Image for Backend
FROM node:20 AS build-backend
WORKDIR /usr/src/app

# Create a user to avoid running as root
RUN useradd -ms /bin/bash appuser
COPY backend/package*.json ./
RUN npm install  # Install dependencies as root to avoid permission issues
COPY backend/ ./
RUN chown -R appuser:appuser /usr/src/app  # Change ownership to appuser

USER appuser  # Switch to appuser for the rest of the process
EXPOSE 3001
CMD ["npm", "start"]

# Final Backend Image
FROM node:20-slim
WORKDIR /usr/src/app
COPY --from=build-backend /usr/src/app ./
EXPOSE 3001
CMD ["npm", "start"]
