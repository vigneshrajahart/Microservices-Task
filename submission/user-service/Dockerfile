# Use Node.js official LTS image
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy all files
COPY . .

# Expose the service port
EXPOSE 3000

# Start the service
CMD ["npm", "start"]
