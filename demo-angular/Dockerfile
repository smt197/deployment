# Stage 1: Build the Angular application
FROM node:22-alpine as builder

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm install

COPY . .

RUN npm run build -- --configuration production

# Stage 2: Serve the application with Nginx
FROM nginx:alpine

# Copy the built Angular application to Nginx's HTML directory
COPY --from=builder /app/dist/vex /usr/share/nginx/html

# Copy your custom Nginx configuration (optional)
# If you have a custom nginx.conf, uncomment the line below and make sure
# your nginx.conf is in the same directory as your Dockerfile.
COPY nginx/nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]