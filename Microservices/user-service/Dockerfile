# Use Node.js official LTS image
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy all files
COPY . .

# Install dependencies
RUN npm install


# Expose the service port
EXPOSE 3000

# Start the service
CMD ["node","app.js"]
