# Step 1: Build React app
FROM node:18 AS build

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json to install dependencies
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the React app's source code
COPY . .
COPY .env .env
# Build the React app for production
RUN npm run build

# Step 2: Serve the app using Nginx
FROM nginx:alpine

# Set environment variable for React's base path
ENV REACT_APP_PUBLIC_URL=/

# Copy the built React app from the previous step to Nginx's default location
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80 (Nginx default port)
EXPOSE 80

# Configure Nginx for single-page app (SPA) handling
# Fallback to index.html for 404s (React Router support)
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Start Nginx to serve the React app
CMD ["nginx", "-g", "daemon off;"]

