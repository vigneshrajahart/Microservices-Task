# Use Node LTS
FROM node:18-alpine

# Set working dir
WORKDIR /app

# Copy dependency files first for better caching
COPY package*.json ./

# Install deps
RUN npm install

# Copy application code
COPY . .

# Expose order service port (defaulting to 3002)
EXPOSE 3002

# Start command (assumes "npm start" exists)
CMD ["npm", "start"]
