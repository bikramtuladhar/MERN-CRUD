# Stage 1: Build the Node.js app
FROM node:alpine as build

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install --production

# Copy the entire application
COPY . .

# Stage 2: Serve the Node.js app with PM2
FROM node:alpine

# Set the working directory
WORKDIR /app

# Copy built files from the previous stage
COPY --from=build /app .

# Install PM2 globally
RUN npm install pm2 -g

# Expose the port on which the Node.js application will run
EXPOSE 8080

ENV MONGODB_URI ""

# Start the Node.js application with PM2
CMD ["pm2-runtime", "index.js", "--update-env"]
