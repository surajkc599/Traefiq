# Using Node:10 Image Since it contains all 
# the necessary build tools required for dependencies with native build (node-gyp, python, gcc, g++, make)
FROM node:12-alpine

ARG HOME_WORK_DIR
ENV HOME_WORK_DIR $HOME_WORK_DIR

# Working directory for docker image
WORKDIR $HOME_WORK_DIR/api-server

# Copy Backend parts dependencies package.json file
COPY package*.json $HOME_WORK_DIR/api-server/

# Necessary to run before adding application code to leverage Docker cache
RUN npm cache clean --force

# Install all packages for Frontend
RUN npm install --quiet

# Copy project directory (locally) in the current directory of our docker image (/api-server)
COPY . .

# Run the web service on container startup
# Expose which environment to pickup from docker-compose file
CMD ["node", "start.js"]