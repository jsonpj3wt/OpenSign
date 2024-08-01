# Stage 1: Build the React application
FROM node:18 AS build
WORKDIR /usr/src/app

# Copy package.json and package-lock.json first to leverage Docker cache
COPY package*.json ./

# Install application dependencies
RUN npm install

# Copy the current directory contents into the container
COPY . .

# Build the React application
RUN npm run build

# Stage 2: Prepare runtime environment
FROM node:18
WORKDIR /usr/src/app

# Copy package.json and package-lock.json to install only production dependencies
COPY package*.json ./

# Install only production dependencies
RUN npm install --only=production

# Copy the build output from the previous stage
COPY --from=build /usr/src/app/build ./build

# Copy .husky folder if necessary
COPY --from=build /usr/src/app/.husky ./.husky

# Make port configurable
ARG PORT=3000
ENV PORT=${PORT}

# Make port available to the world outside this container
EXPOSE ${PORT}

# Run the application
ENTRYPOINT npm run start