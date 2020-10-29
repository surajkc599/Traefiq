# Using Node:12y Image Since it contains all 
# the necessary build tools required for dependencies with native build (node-gyp, python, gcc, g++, make)
FROM node:12-alpine

ARG HOME_WORK_DIR
ENV HOME_WORK_DIR $HOME_WORK_DIR

# Working directory for docker image
WORKDIR $HOME_WORK_DIR/frontend

# Build Frontend part
COPY frontend/package*.json $HOME_WORK_DIR/frontend/

# Necessary to run before adding application code to leverage Docker cache
RUN npm cache clean --force

# Install all packages for Frontend
RUN npm install --quiet

RUN npm install -g http-server

# Copy or project directory (locally) in the current directory of our docker image (/monteurs/frontend)
COPY frontend/ $HOME_WORK_DIR/frontend/

# Build the app for specified environment specified by docker-compose
ARG NODE_ENV
ARG SERVER_PORT
ENV NODE_ENV $NODE_ENV
ENV SERVER_PORT $SERVER_PORT

RUN npm run build

# Run the service on container startup
ENTRYPOINT -Dport=${NODE_ENV} dist/http-server --port ${port}
