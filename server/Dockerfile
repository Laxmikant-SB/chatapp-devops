# Use official Node.js image
FROM node:20-alpine

# Set working directory inside container
WORKDIR /app

# Copy package files first (for caching)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy rest of the server code
COPY . .

# Expose the port the app runs on
EXPOSE 5000

# Command to run the app
CMD ["npm", "start"]
