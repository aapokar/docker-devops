# docker-devops
mooc palautusrepositorio. Kolmas osio jää pysyvästi kesken, mutta 2op kriteerit täyttyvät.

## 1.1
* CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                        PORTS               NAMES
* c9730be92cc3        nginx               "nginx -g 'daemon of…"   19 minutes ago      Exited (0) 16 minutes ago                         gifted_pike
* 68716b732fc6        ubuntu:16.04        "sh -c 'while true; …"   21 minutes ago      Exited (137) 15 minutes ago                       looper
* d3548228c0bf        nginx               "nginx -g 'daemon of…"   31 minutes ago      Up 31 minutes                 80/tcp              charming_fermat

## 1.2
* ]0;pi@akpi: ~[01;32mpi@akpi[00m:[01;34m~ $[00m ls`docker ps -a`
* CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
* ]0;pi@akpi: ~[01;32mpi@akpi[00m:[01;34m~ $[00m docker ps -als[K`docker ps -aimages`
* REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
* ]0;pi@akpi: ~[01;32mpi@akpi[00m:[01;34m~ $[00m quit

## 1.3 
command: `basics`
* You found the correct password. Secret message is:\n"This is the secret message"

## 1.4
`docker run -d devopsdockeruh/exec_bash_exercise`
`docker exec peaceful_williams tail -f ./logs.txt`
Secret message is:
"Docker is easy"

## 1.5
To run the container:
`docker run --rm -it --name vepsite ubuntu:16.04 sh -c 'apt-get update; apt-get install curl; echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'`

The ubuntu container was missing curl, so first 
`apt-get update`
and
`apt-get install curl`
was the proper fix.

## 1.6
`docker run docker-clock`
given command to the container is -c
(files in folder)

## 1.7
command to run the container:
`docker run -it curlerv1`
(files in folder)

## 1.8
* ~:$ `touch logs.txt`
`docker run -v $(pwd)/logs.txt:/usr/app/logs.txt devopsdockeruh/first_volume_exercise`

## 1.9
* `docker pull devopsdockeruh/ports_exercise`
* `docker run -p 5000:80 devopsdockeruh/ports_exercise`

received:
Ports configured correctly!!

## 1.10
* FROM ubuntu

* RUN apt-get update && apt-get install -y curl
* RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
* RUN apt-get install -y nodejs
* RUN apt-get install git -y
* RUN git clone https://github.com/docker-hy/frontend-example-docker.git
* WORKDIR /frontend-example-docker
* RUN npm install
* EXPOSE 5000
* CMD npm run start
(2 files in folder)

## 1.11
`docker run -p 8000:8000 -v $(pwd)/logs.txt:/app/logs.txt backdock`
(file in folder)

## 1.12

Running backend:

* `docker run -p 8888:8000 -e FRONT_URL=http://localhost:5000 backdock`

Running frontend:

* `docker run -p 5000:5000 -e API_URL=http://localhost:8888 frot`
(2 files in folder)

## 1.13
To run the container

* `docker run -p 8080:8080 javaex`

## 1.14 
I changed ruby version in Gemfile and added gems execjs and therubyracer

* `ruby 2.6.0 -> 2.6.6`

## 1.15 
* https://hub.docker.com/r/aapokar/react-anecdote-simple-app

## 1.16
* https://anekdotes1.herokuapp.com/
(file in folder)

# OSA 2

Complete submissions are in their folders

## 2.1

* services:
*  logger-volume:
*    image: devopsdockeruh/first_volume_exercise
*    build: .
*    volumes: 
*      - ./logs.txt:/usr/app/logs.txt
*    container_name: logger

## 2.2 

* services:
*  first-webservice:
*    image: devopsdockeruh/ports_exercise
*    ports: 
*      - 80:80
*    container_name: webber

## 2.3

* services:
*  front:
*    image: frot
*    ports: 
*      - 5000:5000
*    environment:
*      - API_URL=http://localhost:8000

*  back:
*    image: backdock
*    ports:
*      - 8000:8000
*    environment:
*      - FRONT_URL=http://localhost:5000

## 2.4 
  

* services:
*  calculator:
*      build: ./calculator
*      image: calculator
*      ports:
*        - 3000:3000
*      container_name: calculator
*  compute1:
*      build: ./compute
*      image: compute
*      environment:
*        - VIRTUAL_HOST=compute.localtest.me
*  compute2:
*      build: ./compute
*      image: compute
*      environment:
*        - VIRTUAL_HOST=compute.localtest.me
*  load-balancer:
*      build: ./load-balancer
*      image: load-balancer
*      volumes: 
*        - /var/run/docker.sock:/tmp/docker.sock:ro
*      ports:
*        - 80:80
*      container_name: load-balancer

## 2.5


* services:
*  front:
*    image: frot
*    ports: 
*      - 5000:5000
*    environment:
*      - API_URL=http://localhost:8000
*  back:
*    image: backdock
*    ports:
*      - 8000:8000
*    environment:
*      - FRONT_URL=http://localhost:5000
*      - REDIS=database
*      - REDIS_PORT=6379
*  database:
*    image: redis

## 2.6


* services:

*  front:
*    image: frot
*    ports: 
*      - 5000:5000
*    environment:
*      - API_URL=http://localhost:8000

*  back:
*    image: backdock
*    ports:
*      - 8000:8000
*    environment:
*      - FRONT_URL=http://localhost:5000
*      - REDIS=redis
*      - REDIS_PORT=6379
*      - DB_USERNAME=postgres
*      - DB_PASSWORD=pwd
*      - DB_HOST=db

*  redis:
*    image: redis    

*  db:
*    image: postgres
*    environment:
*      - POSTGRES_PASSWORD=pwd
*      - POSTGRES_USER=postgres

## 2.7


* services: 

*    frontend:
*      image: kurkkufront
*      ports:
*        - 3000:3000

*    backend:
*      image: kurkkuback
*      volumes:
*        - ./src/model:/src/model
      
*    training:
*      image: kurkkutrain
*      volumes:
*        - ./src/model:/src/model
*        - ./src/imgs:/src/imgs 

## 2.8 

* services:

*  front:
*    image: frot
*    ports: 
*      - 5000:5000
*    environment:
*      - API_URL=http://localhost:8000

*  back:
*    image: backdock
*    ports:
*      - 8000:8000
*    environment:
*      - FRONT_URL=http://localhost:5000
*      - REDIS=redis
*      - REDIS_PORT=6379
*      - DB_USERNAME=postgres
*      - DB_PASSWORD=pwd
*      - DB_HOST=db

*  redis:
*    image: redis    

*  db:
*    image: postgres
*    environment:
*      - POSTGRES_PASSWORD=pwd
*      - POSTGRES_USER=postgres

*  nginx:
*    image: nginx:alpine
*    ports:
*      - 8080:80
*    volumes:
*      - ./nginx.conf:/etc/nginx/nginx.conf

## 2.9

* services:

*  front:
*    image: frot
*    ports: 
*      - 5000:5000
*    environment:
*      - API_URL=http://localhost:8000

*  back:
*    image: backdock
*    ports:
*      - 8000:8000
*    environment:
*      - FRONT_URL=http://localhost
*      - REDIS=redis
*      - REDIS_PORT=6379
*      - DB_USERNAME=postgres
*      - DB_PASSWORD=pwd
*      - DB_HOST=db

*  redis:
*    image: redis    

*  db:
*    image: postgres
*    environment:
*      - POSTGRES_PASSWORD=pwd
*      - POSTGRES_USER=postgres
*    volumes:
*      - ./database:/var/lib/postgresql/data

*  nginx:
*    image: nginx:alpine
*    ports:
*      - 80:80
*    volumes:
*      - ./nginx.conf:/etc/nginx/nginx.conf

## 2.10

* I set the FRONT_URL here in docker-compose.yml, I had to change it to match the nginx port

  
* services:

*  front:
*    image: frot
*    ports: 
*      - 5000:5000
*    environment:
*      - API_URL=http://localhost:8000

*  back:
*    image: backdock
*    ports:
*      - 8000:8000
*    environment:
*      - FRONT_URL=http://localhost
*      - REDIS=redis
*      - REDIS_PORT=6379
*      - DB_USERNAME=postgres
*      - DB_PASSWORD=pwd
*      - DB_HOST=db

*  redis:
*    image: redis    

*  db:
*    image: postgres
*    environment:
*      - POSTGRES_PASSWORD=pwd
*      - POSTGRES_USER=postgres
*    volumes:
*      - ./database:/var/lib/postgresql/data

*  nginx:
*    image: nginx:alpine
*    ports:
*      - 80:80
*    volumes:
*      - ./nginx.conf:/etc/nginx/nginx.conf
