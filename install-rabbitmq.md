1) Сначала установить все необходимые зависимости с помощью следующей команды:

```
apt-get install gnupg2 curl wget apt-transport-https software-properties-common -y
```

2) После установки всех зависимостей загрузить и установить пакет репозитория Erlang с помощью следующей команды:

```
wget https://packages.erlang-solutions.com/erlang/debian/pool/esl-erlang_23.1.5-1~debian~stretch_amd64.deb

dpkg -i esl-erlang_23.1.5-1~debian~stretch_amd64.deb
```
Для исправления ошибок зависимости выполнить следующую команду:

```
apt-get install -f
```
3) Обновить репозиторий Erlang и установить пакет Erlang с помощью следующей команды:

```
apt-get update -y
apt-get install erlang erlang-nox
```
4) Добавить репозиторий RabbitMQ с помощью следующей команды:

```
add-apt-repository 'deb http://www.rabbitmq.com/debian/ testing main'
wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | apt-key add -
```
5) После добавления репозитория обновить репозиторий с помощью следующей команды:

```
apt-get update -y
```

Установка сервера RabbitMQ

6) Теперь можно установить сервер RabbitMQ, выполнив следующую команду:

```
apt-get install rabbitmq-server -y
```
7) После завершения установки запустить службу RabbitMQ и включить ее запуск при перезагрузке системы:

```
systemctl start rabbitmq-server
systemctl enable rabbitmq-server
````
8) Проверить статус службы RabbitMQ, используя следующую команду:

```
systemctl status rabbitmq-server
```

9) Создать пользователя-администратора для RabbitMQ с помощью следующей команды:

```
rabbitmqctl add_user admin password
```
10) Установить тег для своей учетной записи администратора, используя следующую команду:

```
rabbitmqctl set_user_tags admin administrator
```
11) Установить правильное разрешение с помощью следующей команды:

```
rabbitmqctl set_permissions -p / admin ".*" ".*" ".*"
```
12) Включить консоль управления RabbitMQ с помощью следующей команды:

```
rabbitmq-plugins enable rabbitmq_management
```

Доступ к информационной панели RabbitMQ

По умолчанию веб-консоль RabbitMQ прослушивает порт 15672. Проверить это можно с помощью следующей команды:

```
ss -antpl | grep 15672
```
следующий вывод:

```

LISTEN 0      1024              0.0.0.0:15672      0.0.0.0:*    users:(("beam.smp",pid=29132,fd=96))    

```
14) Теперь можно открыть веб-браузер и получить доступ к веб-консоли RabbitMQ, используя URL-адрес:

```
http://your-server-ip:15672/
```
