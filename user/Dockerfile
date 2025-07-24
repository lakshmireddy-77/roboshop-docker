FROM node:20
WORKDIR /opt/server/
COPY package.json .
COPY *.js .
RUN npm install
ENV MONGO="true" \
    REDIS_URL="redis://<REDIS-IP-ADDRESS>:6379" \
    MONGO_URL="mongodb://<MONGODB-SERVER-IP-ADDRESS>:27017/users"
CMD [ "node", "server.js" ]