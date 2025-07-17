FROM node:20
# i am giving this my wkd
WORKDIR /opt/server
# copy the files . means pwd
COPY package.json .
COPY server.js .
# installing depenidies
RUN npm install
ENV MONGO=true \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
# start the service ExecStart=/bin/node /app/server.js
# we alraeady in server floder 
CMD ["node","server.js"]