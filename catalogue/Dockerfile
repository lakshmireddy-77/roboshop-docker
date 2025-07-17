FROM node:20
# i am giving this my wkd
WORKDIR /opt/server
# copy the files . means pwd
COPY package.json .
COPY server.js .
# installing depenidies
RUN npm install
ENV MONGO=true \
    REDIS_URL="'redis://redis:6379'"\
    MONGO_URL="mongodb://mongodb:27017/users"
# start the service ExecStart=/bin/node /app/server.js
# we alraeady in server floder 
CMD ["node","server.js"]