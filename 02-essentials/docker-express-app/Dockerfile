# Use the official Node.js 22 Alpine image as the base image
FROM node:22-alpine

# Set the working directory inside the container to /app
WORKDIR /app

# Copy package.json and package-lock.json (if present) to the working directory
COPY package*.json ./

# Install all dependencies defined in package.json
RUN npm install

# Copy the rest of the application source code to the working directory
COPY . .

# Set environment variable for the application port
ENV PORT=3000

# Define the command to run the application
CMD ["npm", "run", "start"]
