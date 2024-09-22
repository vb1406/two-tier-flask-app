 
# Flask App with MySQL Docker Setup

This is a simple Flask app that interacts with a MySQL database. The app allows users to submit messages, which are then stored in the database and displayed on the frontend.

## Prerequisites
- Docker
- Git (optional, for cloning the repository)

## Setup  - For Ubuntu, install docker
sudo apt install
sudo apt update
sudo apt install docker.io
sudo chown $USER /var/run/docker.sock
docker ps


## Download app from github
git clone https://github.com/vaibhav.b1406/two-tier-flask-app.git
cd two-tier-flask-app
docker build . -t flaskapp
docker images

## Create docker volume
docker volume create mysql-data

## Create docker network 
docker network create twotier

 ## backend container
 docker run -d --name=mysql --network=twotier -v mysql-data:/var/lib/mysql -e MYSQL_DATABASE=devops -e MYSQL_ROOT_PASSWORD=root mysql:5.7

## app container
 docker run -d --name=flaskapp -p 5000:5000 --network=twotier -e MYSQL_HOST=mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=root -e MYSQL_DB=devops flaskapp:latest

## Use the Ip and add the port to :5000


