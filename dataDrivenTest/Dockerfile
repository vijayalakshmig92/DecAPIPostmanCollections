# Use the official Node.js 16 image as the base image
FROM node:16

# Set the working directory in the container
WORKDIR /app

# Install Newman globally
RUN npm install -g newman

# Install Newman html report
RUN npm install -g newman-reporter-html

# Install Newman Reporter HTMLExtra
RUN npm install -g newman-reporter-htmlextra

# Copy your Postman collection and environment files to the working directory
COPY DataDriverAPIs.json .
COPY GoRestEnv.json .
COPY myUser.csv .

# Set the command to run Newman and execute your Postman collection
CMD ["newman", "run", "DataDriverAPIs.json", "-e", "GoRestEnv.json", "-d", "myUser.csv",  "-r", "cli,json,html,htmlextra"]