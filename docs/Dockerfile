# Build stage
FROM node:20-alpine AS builder

WORKDIR /slidev

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application
COPY . .

# Build the static site
RUN npm run build

# Production stage
FROM nginx:alpine

# Copy the built files from builder stage
COPY --from=builder /slidev/dist /usr/share/nginx/html
COPY --from=builder /slidev/images /usr/share/nginx/html/images

# Copy custom nginx configuration
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
