# Build Stage
FROM node:latest as builder

# Set node environment to production
ENV NODE_ENV production

# Set working directory
WORKDIR /app

# Cache and Install dependencies
COPY package.json .
COPY yarn.lock .
# Adding openssl compatibility support
ENV NODE_OPTIONS "--openssl-legacy-provider"
RUN yarn install --silent --production

# Copy app files
COPY . .

# Build the app
RUN yarn build


# Bundle and serve using Nginx
FROM nginx:alpine as production
ENV NODE_ENV production

# Copy build files from builder
COPY --from=builder /app/build /usr/share/nginx/html

# Add your nginx.conf
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]