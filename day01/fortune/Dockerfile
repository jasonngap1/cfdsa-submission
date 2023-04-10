FROM node:19

# mkdir /app && cd /app
WORKDIR /app

# copy the files from the current directory to the container
COPY main.js .
COPY package.json .
COPY package-lock.json .

COPY public public
COPY views views

# install dependencies
# using ci instead of install to avoid updating package-lock.json, will use the packages mentioned in package-lock.json
# difference between this and ["npm", "install"] is that the latter will use a shell to run commands
RUN npm ci

# RUN
# this is your application port, whatever port is binded to this port is used to access the application. for example 8080:3000 means you go to localhost:8080 to access the application
ENV APP_PORT=3000

HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
    CMD curl localhost:${APP_PORT}/health || exit 1

EXPOSE ${APP_PORT}

ENTRYPOINT node main