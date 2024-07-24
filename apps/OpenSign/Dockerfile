# Use an official Node runtime as the base image
FROM node:18

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json first to leverage Docker cache
COPY ./package*.json ./

# Install application dependencies
RUN npm install

# Copy the current directory contents into the container
COPY ./ .
COPY ./.husky .

# Make port configurable
ARG PORT=3000
ENV PORT=${PORT}

# Build the React application
RUN npm run build

# Make port available to the world outside this container
EXPOSE ${PORT}

# Run the application
ENTRYPOINT npm run start