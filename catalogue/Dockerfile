FROM node:20-alpine3.21
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server/
COPY package.json . 
COPY *.js .
RUN chown -R roboshop:roboshop /opt/server
USER roboshop
RUN npm install
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"

CMD [ "node", "server.js" ]
