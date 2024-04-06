FROM node:16

# Set app directory
WORKDIR /app

# Set node environment to production
ENV NODE_ENV production

# Add netcat to be able to wait for other services with scripts
RUN apt-get update
RUN apt-get install -y netcat-traditional bash

# Install dependencies
COPY package.json .
RUN npm install --production --silent

# Copy project files
COPY . .

# Start backend
CMD sh ./src/scripts/wait-for-mongo.sh && npm run seed && npm run dev