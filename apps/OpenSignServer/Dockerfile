# Use an official Node runtime as the base image
FROM node:20

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json first to leverage Docker cache
COPY package*.json ./

# Install application dependencies
RUN npm install

# Copy the current directory contents into the container
COPY . .

# Build the application (uncomment if you have a build step)
# RUN npm run build

# Stage 2: Prepare runtime environment
FROM node:18
WORKDIR /usr/src/app

# Copy package.json and package-lock.json to install only production dependencies
COPY package*.json ./

# Install only production dependencies
RUN npm install --only=production

# Copy the necessary files from the build stage
COPY --from=build /usr/src/app .

# Make port configurable
ARG PORT=8080
ENV PORT=${PORT}

# Make port available to the world outside this container
EXPOSE ${PORT}

# Run the application
ENTRYPOINT npm start