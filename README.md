# roboshop-docker

ROBOSHOP:
==========
mongodb --7 version ---> official image fromdocker hub 
we will take it from docker hub 
initializing a fresh instance:
when a container is started 1st time it will execute files with .sh and .js that found in the location 
/docker/entrypoint-initdb.d 
files will be executed in alphabatical order
start,stop,and data loading ---> all will come from image
docker build -t mongodb:v1 .
docker images
docker run -d --name mongodb mongodb:v1
here 
-p ---> is not given bacuse we are not exposed outside
docker ps ----> mongodb is runnng
--------------------------------------------
docker build -t catalogue:v1 .
docker images
docker run -d --name catalogue catalogue:v1
docker ps
docker exec -it catalogue bash
curl http://localhost:8080/health  ---> sucess mesans catalogue runnng fine 
failure:
=======
docker logs catalogue
ipconfig 
who will provid the internet to vm ---> aws --> this is ethernet port 
here we are installing docker so docker inetrenally/viruvally created one network ---> this is called docker o ---> This is like mode M.
whenever we are creating docker container it will allocate the IP 
docker modem ---> (172.17.0.1)
docker inspect catalogue ---> It contain one IP (172.17.0.2)
docker inspect mongodb ---> It contain one IP (172.17.0.3)
Here those are in same network but unable to connect. Beacause docker uses default network
docker network docker netrwork ls ---> To see the list of networks

there are 2 types of networks:
bridge network
host network
Docker by default bridge network 
ex: docker 0 is the bridge that allocates Ip to components --> called bridge
host network:
modem gives the IP to the components. It will directly connected with host network
by deafult docker created bridge network whenever you installed docker inside any server
we can create sepaarte network beacuse both componets are not connected by default


host means directly host network.
bridge means docker create separate network interface and assign the IP address to conatiners.
docker default network can't comminucate between conatainers
docker always suggest to create custom bridge network


docker network create roboshop ----> to crate network
before connectining we need to disconnect:
docker network disconnect bridge catalogue
docker network disconnect bridge mongodb
docker network ls
docker network connect roboshop mongodb
docker network connect roboshop catalogue
docker inspect mongodb
docker inspect catalogue
docker exec -it catalogue bash
cutl localhost:8080/health 
# now it is connected
here we need to use customized network

-------------------
redis:
here we are installing redis, not filling the data. so we can run directly
docker run -d --name redis --network roboshop redis:7.
there is no local image so it can directly pull the image fom hub
docker ps ---It is running

--------------------
user:
docker build -t  user:v1 .
docker run -d --name user --network roboshop user:v1
docker ps
docker exec -it user
curl localhost 8080

-----------------------
cart:

docker build -t cart:v1
docker run -d --name cart --network roboshop cart:v1
docker ps
docker exec -it cart
curl localhost 8080

---------------------
mysql:

docker build -t mysql:v1
docker run -d --name mysql --network roboshop mysql:v1
docker ps
docker exec -it mysql

-----------------
shipping:

docker build -t shipping:v1
docker run -d --name shipping --network roboshop shipping:v1
docker ps
docker exec -it shipping
curl localhost 8080

-------------------------------next day
docker login -u lakshmi315
for i in cart catalogue mongodb mysql shipping user; do cd $i; docker build -t joindevops/$i:v1 . ; docker push lakshmi315/$i ; cd .. ; done    

docker compose:
================
it is a command line tool for  multi container application
we can define all docker containers as service. 
create dependies b/w them start them at onces and stop them at onces 
- start and stop, rubuild the services 
- view the status of running services
- stream the log output of running services

here catalogue depends on momgodb
cart depends on catalogue 

here we we run cart without catalogue and db the applications is not run. and we need to remebers the flow which we need to run 1st
so instead of we have docker compose

what is our run command:
-----------------------
docker run -d --name mongodb --network roboshop joindevops/mongodb:v1

docker compose up -d 

-d ---> sending to background

docker ps 

when ever we chang the files we need again run 
docker compose up -d 

----------------------
payment:

docker build -t lakshmi315/payment:v1
# we can give environemnt variables on run time or build time
docker compose up -d 

--------------------
frontend:

