# Multistage Dockerfile

# Stage1: First stage will build the artifact
FROM node:14 AS web-build
WORKDIR /usr/src/app
COPY ./ ./client
# this copies the entire client folder contents in local workspace into a client directory 
# on this Stage1 builder container. The full container directory is /usr/src/app/client
# since WORKDIR is /usr/src/app
RUN cd client && npm install && npm run build --prod
# npm install will install all the dependencies that are required as noted in package.json
# npm run build will then run the build script and build the artifact for this application
# The artifact will be in the /usr/src/app/client directory and this needs to be copied into the
# Stage2 container below which will run this app that was just built.....
# We will be hosting this angular app on an nginx docker instance as indicated below....


# Stage2: Copy the artifact above into the  main image --from=web-build above
# Use official nginx image as the base image
FROM nginx:latest

# Copy the build output to replace the default nginx contents.
COPY --from=web-build /usr/src/app/client/dist/client/ /usr/share/nginx/html
# the /usr/src/app/client/dist/clent is the path to the artifact built above in Stage1
# This content (html files)is copied into the /usr/share/ngnix/html directory on this Stage2 container
# This is our artifact angular build.  nginx uses this /usr/share/nginx/html to serve up the html content
COPY nginx.conf /etc/nginx/conf.d/default.conf
# nginx.conf is in my local worspace. This is a customized configuration for this app.

# Expose port 4200
EXPOSE 4200
