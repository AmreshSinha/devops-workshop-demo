FROM node:latest

# Set app directory
WORKDIR /app

# Set node environment to production
ENV NODE_ENV production

# Add netcat to be able to wait for other services with scripts
RUN apt-get update
RUN apt-get install -y netcat-traditional

# Install dependencies
COPY package.json .
RUN npm install --production --silent
RUN npm install nodemon -g --silent

# Copy project files
COPY . .

# Start backend
CMD sh ./src/scripts/wait-for-mongo.sh && npm run seed && npm run dev