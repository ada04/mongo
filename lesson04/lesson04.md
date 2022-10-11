# Ответ на ДЗ 4
Базовые запросы к MongoDB

**Установка mongo**
* Для установки сервера был выбран домашний сервер с Ubuntu 20.04

**установка mongo**
```bash
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
apt update
apt-get install -y mongodb-org
sudo systemctl start mongod
sudo systemctl status mongod
```

**проверяем подключение**

mongosh --port 27017

```sql
Current Mongosh Log ID: 634509ca35e0f3fa231a5464
Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+1.6.0
Using MongoDB:          6.0.2
Using Mongosh:          1.6.0

For mongosh info see: https://docs.mongodb.com/mongodb-shell/

test>
```

**создаем пользователя**
```sql
test> use admin
switched to db admin
admin> db.createUser( { user: "root", pwd: "otus", roles: [ "userAdminAnyDatabase", "dbAdminAnyDatabase", "readWriteAnyDatabase" ] } )
{ ok: 1 }
```

**Правим mongod.conf**
```bash
security:
  authorization: enabled
net:  
  bindIpAll: true
```

**перезапускаем сервер**

```bash
sudo systemctl restart mongod
```

**Пропишем подлкючение для Compass**

mongodb://root:otus@192.168.1.16:27017/

**Восстановим коллекцию с бсоном**
_не сразу понял как указать базу данных, в которую необходимо загрузить коллекцию. Оказалось, что в строке подключения указывается БД в которой создан пользователь, а аргументом передается имя БД для коллекции..._

mongorestore --uri='mongodb://root:otus@127.0.0.1:27017/?authSource=admin&directConnection=true' -d orders -c people --verbose people.bson



**Подключение прошло успешно**

В процессе выполнения столкнулся с проблемой запуска сервера Mongo v5+ на процессоре Celeron (в штатной сборке не поддерживается) перешёл на другой ПК и проблема решилась.
