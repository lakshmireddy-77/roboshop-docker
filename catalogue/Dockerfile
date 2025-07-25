FROM node:20-alpine3.21
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server/
COPY package.json .
COPY *.js .
RUN npm install
RUN chown -R roboshop:roboshop /opt/server

ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
USER roboshop
# Run app
CMD ["node", "server.js"]
