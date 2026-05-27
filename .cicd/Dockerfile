FROM node:14

#Creates a build variable.
ARG SRC_DIR=/opt/i27
# Create a directory(/opt/i27) inside the container  image
RUN mkdir -p $SRC_DIR

# Set the working directory for all next commands.
WORKDIR $SRC_DIR


# Copies our application files(surrent directory) from local machine into image(under /opt/i27/).
COPY . $SRC_DIR

# Install node.js dependencies
RUN npm install 

# Expose the port(This container application listens on port 3000)
EXPOSE 3000 

# Copies entrypoint script into container root filesystem.
COPY ./.cicd/entrypoint.sh /entrypoint.sh

# make the entrypoint.sh script executable
RUN chmod +x /entrypoint.sh

CMD ["/entrypoint.sh"]

# CMD ["java", "-jar", "/opt/i27/i27-users.jar"] java application


# means: When container starts, run /entrypoint.sh

# So container startup flow becomes:

# Container Starts
#         ↓
# /entrypoint.sh executes
#         ↓
# script checks environment argument
#         ↓
# runs npm command
#         ↓
# Node app starts 

# Example 1: if Container runs: /entrypoint.sh Then: $1 = empty So: ENVIRONMENT=dev Then script runs: npm run start:dev
# Example 2: if Container runs: /entrypoint.sh prod Then: $1=prod So: ENVIRONMENT=prod Then script runs: npm run start:prod

