# Ответ на ДЗ 3
Установка Docker и создание БД MongoDB в контейнере

**Установка Docker**
* Для установки сервера был выбран домашний сервер с Ubuntu 20.04

-- поставим докер
sudo apt-get update && sudo apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo apt-key fingerprint 0EBFCD88 && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && sudo apt-get update && sudo apt-get install -y docker-ce docker-ce-cli containerd.io

-- https://www.mongodb.com/compatibility/docker
-- 1. Создаем docker-сеть: 
sudo docker network create mongo-net

-- 2. подключаем созданную сеть к контейнеру сервера MongoDB:
sudo  docker run --name mongo-server --network mongo-net -d -p 27017:27017 -v /home/aeugene/mongo:/data/db mongo:5.0.4

sudo docker inspect mongo-server | grep IPAddress 

-- 3. Запускаем отдельный контейнер с клиентом в общей сети с БД: 
sudo docker run -it --rm --name mongo-client --network mongo-net mongo:5.0.4 mongo mongo-server
sudo docker run -it --rm --name mongo-client --network mongo-net mongo:5.0.4 mongo 172.18.0.2

-- 4. Проверяем, что подключились через отдельный контейнер:
sudo docker ps -a

-- учтите, порт торчит наружу!!!
ss -tlpn

sudo apt install net-tools -y
netstat -a | grep mongo

mongo 172.18.0.2:27017 -u root -p otus\$123 --authenticationDatabase admin

sudo docker stop mongo-server
sudo docker rm mongo-server

Read more [here](./lesson03.log)

**Подключение прошло успешно**

В процессе выполнения столкнулся с проблемой запуска сервера Mongo v5+ на процессоре Celeron (в штатной сборке не поддерживается) перешёл на другой ПК и проблема решилась.
