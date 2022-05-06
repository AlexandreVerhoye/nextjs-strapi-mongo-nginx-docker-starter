# Base on offical Node.js Alpine image
FROM node:alpine

# Set working directory
WORKDIR /usr/app

# Install PM2 globally
RUN npm install --global pm2

# Install module dependencies via apk
# https://github.com/nodejs/docker-node/issues/282
#RUN apk update && apk add python g++ make && rm -rf /var/cache/apk/*

# Copy package.json and yarn.json before other files
COPY package.json yarn.lock /usr/app/
RUN yarn install --frozen-lockfile

# Install app dependencies via yarn
RUN yarn --production

# Copy all files
COPY . /usr/app/

# Build App
RUN yarn build

# Expose the listening port
EXPOSE 3000

# Give node user write permission for app
RUN chown -R node .

# Run container as non-root (unprivileged) user
# The node user is provided in the Node.js Alpine base image
USER node

# Run npm start script with PM2 when container starts
CMD ["pm2-runtime", "start", "yarn", "--interpreter", "sh", "--name", "web-interface", "--", "start"]