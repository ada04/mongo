# Ответ на ДЗ 2
Cоздание БД MongoDB 

**Установка сервера MongoDB**
* Для установки сервера был выбран домашний сервер с Ubuntu 20.04
Установку производил командами из приложенного файла. Наcтроил авторизацию ssh по ключу

```bash
ada@MacBook-Air-Dmitrij ~ % cat /etc/hosts                
##
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1	localhost
255.255.255.255	broadcasthost
::1             localhost
192.168.1.27	mongo_home
ada@MacBook-Air-Dmitrij ~ % ssh vagrant@mongo_home -i .ssh/id_rsa_mongo 
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-84-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Wed 14 Sep 2022 12:53:46 PM MSK

  System load:  0.05               Processes:             114
  Usage of /:   16.5% of 61.31GB   Users logged in:       1
  Memory usage: 30%                IPv4 address for eth0: 192.168.1.27
  Swap usage:   0%


Base box built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
Python 3.8.10 virtualenv with data processing and Machine Learning packages
available at /opt/ipnb

Last login: Wed Sep 14 12:37:22 2022 from 192.168.1.18
vagrant@vgr-ipnb-simple:~$ 
```

* После настроек БД проведена проверка удалённого подключения.
На ноутбуке установлен клиент версии 5, а сервер 4.4, в связи с чем был варнинг    

```bash
ada@MacBook-Air-Dmitrij .ssh % mongo 192.168.1.27:27001 -u root -p otus$123 --authentificationDatabase admin
Error parsing command line: unrecognised option '--authentificationDatabase'
try 'mongo --help' for more information
ada@MacBook-Air-Dmitrij .ssh % mongo 192.168.1.27:27001 -u root -p otus$123 --authenticationDatabase admin 
MongoDB shell version v5.0.11
connecting to: mongodb://192.168.1.27:27001/test?authSource=admin&compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { id : UUID(b71ec59f-28eb-4c43-bfdd-37901c681509) }
MongoDB server version: 4.4.16
WARNING: shell and server versions do not match
================
Warning: the mongo shell has been superseded by mongosh,
which delivers improved usability and compatibility.The mongo shell has been deprecated and will be removed in
an upcoming release.
For installation instructions, see
https://docs.mongodb.com/mongodb-shell/install/
================
Welcome to the MongoDB shell.
For interactive help, type help.
For more comprehensive documentation, see
	https://docs.mongodb.com/
Questions? Try the MongoDB Developer Community Forums
	https://community.mongodb.com
> use test
switched to db test
> db.peoples.find()
{ _id : ObjectId(63219cef217362d90c6f59a2), Name : Mickey }
> 
```

**Подключение прошло успешно, БД готова к использованию**
