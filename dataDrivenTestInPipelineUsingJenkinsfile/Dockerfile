# Use the official Node.js 16 image as the base image
FROM node:25

# Set the working directory in the container
WORKDIR /app

# Install Newman globally
RUN npm install -g newman

# Install Newman html report
RUN npm install -g newman-reporter-html

# Install Newman Reporter HTMLExtra
RUN npm install -g newman-reporter-htmlextra

# Ensure the result directory exists
RUN mkdir -p /app/results

# Copy your Postman collection and environment files to the working directory
COPY DataDriverAPIs.json .
COPY GoRestEnv.json .
COPY myUser.csv .

# Set the command to run Newman and execute your Postman collection
CMD ["newman", "run", "/app/DataDriverAPIs.json", "-e", "/app/GoRestEnv.json", "-d", "/app/myUser.csv",  "-r", "cli,json,html,htmlextra", "--reporter-htmlextra-export", "./results/Datadriven.html"]