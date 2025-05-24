# Use an official image of Node.js runtime
FROM node:22-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy all package.json files in the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

COPY . .

ENV PORT=3000

CMD ["npm", "run", "start"]
