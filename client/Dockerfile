# Use the official Node.js image as the base image (updated to node:20 for compatibility)
FROM node:20 AS build

# Set the working directory inside the container
WORKDIR /usr/src/app

# Create a non-root user and switch to it
RUN useradd -ms /bin/bash appuser
USER appuser

# Copy the package.json and package-lock.json first (for efficient caching)
COPY client/package*.json ./

# Install dependencies using npm ci for a clean environment (instead of npm install)
RUN npm ci

# Ensure react-scripts has the correct permissions
RUN chmod +x node_modules/.bin/react-scripts

# Install additional dependencies like axios and Babel plugin if needed
RUN npm install axios --save
RUN npm install @babel/plugin-proposal-private-property-in-object --save-dev

# Copy the rest of the application code
COPY client/ .

# Build the React app
RUN npm run build

# Expose the app port (if necessary)
EXPOSE 3000

# Command to start the app (for production environment)
CMD ["npm", "start"]
