FROM node:20 AS build
WORKDIR /usr/src/app

# Create user
RUN useradd -ms /bin/bash appuser
USER root  # Temporarily use root user to install dependencies

# Ensure appuser has ownership of the entire working directory
RUN chown -R appuser:appuser /usr/src/app

USER appuser  # Switch back to appuser

# Copy package.json and package-lock.json files with correct ownership
COPY --chown=appuser:appuser client/package*.json ./

# Install dependencies
RUN npm install

# Install additional dependencies like axios and Babel plugin if needed
RUN npm install axios --save
RUN npm install @babel/plugin-proposal-private-property-in-object --save-dev

# Copy the rest of the application
COPY client/ ./

# Build the React app
RUN npm run build

# Expose the app's port
EXPOSE 3000

# Start the application
CMD ["npm", "start"]
