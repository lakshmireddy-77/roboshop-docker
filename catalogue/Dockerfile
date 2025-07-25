FROM node:20-alpine3.21

# Create non-root user
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop

# Set working directory
WORKDIR /opt/server/

# Copy files as root and fix ownership
COPY package.json .
COPY *.js .

RUN chown -R roboshop:roboshop /opt/server

# Switch to non-root user before install
USER roboshop

# Install dependencies
RUN npm install

# Environment variables
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"

# Run app
CMD ["node", "server.js"]
