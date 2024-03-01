# Multistage
# Stage1: builds the artifact.  
FROM node:14 AS nodeapi-build
WORKDIR /usr/src/app
COPY ./ ./nodeapi/
# Copy the entire nodeapi local workspace folder to /usr/src/app/nodeapi folder on this builder container
RUN cd nodeapi && npm install
# go into the nodeapi directory with the nodejs source code and install the dependencies. This will build
# the nodejs application artifact.


# Stage2: the nodejs container
FROM node:14
WORKDIR /usr/src/app/
COPY --from=nodeapi-build /usr/src/app/nodeapi/ ./
# Copy the artifact from Stage1 above to the /sur/src/app/ directory of this nodejs container
RUN ls
EXPOSE 5000
CMD ["/bin/sh", "-c", "cd /usr/src/app/ && npm start"]
# This will start the nodejs app on the stage2 docker container
# The node app will be started.
# Test3
