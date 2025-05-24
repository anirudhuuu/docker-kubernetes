# Use a slimmer Alpine-based Node.js image
FROM node:22-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy dependency definition files to the working directory
COPY package*.json ./

# Alternatively, you can use that will not be cached
# COPY package.json ./
# COPY package-lock.json ./

# Install project dependencies
RUN npm install

# Copy the rest of the application source code to the container
COPY . .

# Expose the port the app runs on
EXPOSE 5173

# Default command to run the development server
CMD ["npm", "run", "dev"]
