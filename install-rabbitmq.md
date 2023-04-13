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


###Установка сервера RabbitMQ

Теперь вы можете установить сервер RabbitMQ, выполнив следующую команду:

apt-get install rabbitmq-server -y
После завершения установки запустите службу RabbitMQ и включите ее запуск при перезагрузке системы:

systemctl start rabbitmq-server
systemctl enable rabbitmq-server
Вы можете проверить статус службы RabbitMQ, используя следующую команду:

systemctl status rabbitmq-server

#Cледующий шаг.

Создать пользователя-администратора для RabbitMQ
Далее вам нужно будет создать пользователя-администратора для RabbitMQ. Вы можете создать его с помощью следующей команды:

rabbitmqctl add_user admin password
Затем установите тег для своей учетной записи администратора, используя следующую команду:

rabbitmqctl set_user_tags admin administrator

Затем установите правильное разрешение с помощью следующей команды:

rabbitmqctl set_permissions -p / admin ".*" ".*" ".*"

Затем включите консоль управления RabbitMQ с помощью следующей команды:

rabbitmq-plugins enable rabbitmq_management


#Следующий шаг.

Доступ к информационной панели RabbitMQ
По умолчанию веб-консоль RabbitMQ прослушивает порт 15672. Вы можете проверить это с помощью следующей команды:

ss -antpl | grep 15672
Вы получите следующий вывод:

LISTEN 0      1024              0.0.0.0:15672      0.0.0.0:*    users:(("beam.smp",pid=29132,fd=96))    

Теперь откройте веб-браузер и получите доступ к веб-консоли RabbitMQ, используя URL-адрес http://your-server-ip:15672/. Вы должны увидеть страницу входа RabbitMQ.

