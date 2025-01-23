FROM node:20 AS build
WORKDIR /usr/src/app

# Create user
RUN useradd -ms /bin/bash appuser
USER appuser

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

# Install a simple static file server (serve)
RUN npm install -g serve

# Expose the app's port
EXPOSE 3000

# Serve the built React app
CMD ["serve", "-s", "build", "-l", "3000"]


