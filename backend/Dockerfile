# backend/Dockerfile
FROM node:20

WORKDIR /app

# Copy package.json and package-lock.json first
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the code
COPY . .

# Expose port
EXPOSE 5050

# Start the server
CMD ["node", "server.js"]
