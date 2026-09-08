University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FTMI](https://ftmi.itmo.ru/)  
Course: [Введение в веб технологии](https://itmo-ict-faculty.github.io/introduction-in-web-tech/)  
Year: 2025/2026  
Group: U4225<br>
Author: Peshkov Andrey Konstantinovich<br>
Lab: Lab 1<br>
Date of create: 08.09.2026  
Date of finished:  

# Лабораторная работа №1

### 0. Скачивание и установка Docker
<img width="1181" height="801" alt="DOCK" src="https://github.com/user-attachments/assets/e2a96d76-471b-4a6d-8ae1-95ce6dccec6e" />

### 1. Проверка установки Docker

Для проверки установленной версии Docker была выполнена команда:

`docker --version`

Получен результат:

Docker version 29.7.2, build a7dcaa6.

Далее был запущен тестовый контейнер:

`docker run hello-world`

Контейнер успешно вывел сообщение `Hello from Docker!`. Это подтверждает, что Docker Engine доступен, а образ был загружен из Docker Hub и запущен.

Также были выполнены команды:

`docker images`  
`docker ps`  
`docker ps -a`

Команда `docker images` показывает скачанные локальные образы. Команда `docker ps` показывает работающие контейнеры. Команда `docker ps -a` показывает все контейнеры, включая остановленные.

<img width="1547" height="837" alt="image_2026-09-07_19-06-01" src="https://github.com/user-attachments/assets/35cc884a-7bc9-4730-a668-ca1aab6d02e2" />


*Рисунок 1 — проверка Docker и запуск тестового контейнера.*

### 2. Работа с образом Ubuntu

Был скачан образ Ubuntu:

`docker pull ubuntu:latest`

После загрузки образ был проверен:

`docker images`

Затем был создан интерактивный контейнер:

`docker run -it --name ubuntu-test ubuntu:latest bash`

Внутри контейнера были обновлены сведения о пакетах и установлен `curl`:

`apt update`  
`apt install -y curl`  
`curl --version`

В выводе `curl --version` указана установленная версия `curl 8.18.0`. После завершения работы был выполнен выход из контейнера:

`exit`

Состояние контейнера проверено командой:

`docker ps -a`

Контейнер `ubuntu-test` сохранился в остановленном состоянии.


<img width="1600" height="1412" alt="image_2026-09-07_19-20-20" src="https://github.com/user-attachments/assets/e488a6a9-a7af-4a5c-9d29-b15305a23a11" />


*Рисунок 2 — запуск контейнера Ubuntu, обновление пакетов и установка curl.*


<img width="1601" height="1408" alt="image_2026-09-07_19-20-36" src="https://github.com/user-attachments/assets/18c56e76-e062-4968-a3d3-d86066560706" />
<img width="1599" height="1406" alt="image_2026-09-07_19-20-56" src="https://github.com/user-attachments/assets/88f540e1-8282-4800-b92d-6c2bfeddf92d" />


*Рисунки 3 и 4 — проверка curl и остановленный контейнер ubuntu-test.*

### 3. Запуск веб-сервера Nginx

Для запуска Nginx был создан контейнер с пробросом порта 8080 хоста на порт 80 контейнера:

`docker run -d -p 8080:80 --name web-server nginx:alpine`

Состояние контейнера проверено:

`docker ps`

В выводе указан проброс портов:

0.0.0.0:8080->80/tcp.

Работа Nginx проверена запросом:

`curl http://localhost:8080`

В ответ была получена стандартная HTML-страница `Welcome to nginx!`.

Также были просмотрены логи контейнера:

`docker logs web-server`

<img width="1259" height="1335" alt="image_2026-09-07_19-26-57" src="https://github.com/user-attachments/assets/4041a322-e584-4ee8-a7ff-8250ba8c7f7f" />


*Рисунок 5 — запуск контейнера Nginx и ответ веб-сервера.*

Для подключения к контейнеру была выполнена команда:

`docker exec -it web-server sh`

Внутри контейнера были выполнены команды:

`nginx -v`  
`ls /usr/share/nginx/html`

Определена версия `nginx/1.31.5`. В каталоге веб-сервера найдены файлы `index.html` и `50x.html`.

<img width="1257" height="394" alt="image_2026-09-07_19-27-29" src="https://github.com/user-attachments/assets/7069938e-dc7e-4e7e-824e-7323655c5784" />


*Рисунок 6 — подключение к контейнеру и проверка Nginx.*

### 4. Управление контейнером

Контейнер Nginx был остановлен:

`docker stop web-server`

После остановки контейнер отсутствовал в выводе `docker ps`, но присутствовал в выводе `docker ps -a`.

Контейнер был запущен повторно:

`docker start web-server`  
`docker ps`

Перед удалением контейнер был остановлен:

`docker stop web-server`  
`docker rm web-server`

После удаления контейнера был удалён образ:

`docker rmi nginx:alpine`

<img width="1252" height="731" alt="image_2026-09-07_19-39-57" src="https://github.com/user-attachments/assets/9dc70590-3179-4ff6-af3b-7407523a980e" />


*Рисунок 7 — управление контейнером web-server и удаление образа nginx:alpine.*

### 5. Работа с Docker Volume

Был создан именованный том:

`docker volume create my-volume`  
`docker volume ls`

Том `my-volume` появился в списке томов.

Затем был запущен контейнер с подключённым томом:

`docker run -dit --name volume-test -v my-volume:/data ubuntu:latest bash`  
`docker exec -it volume-test bash`

Внутри контейнера создан файл в подключённом томе:

`echo "Hello from volume" > /data/test.txt`  
`cat /data/test.txt`

Файл содержал текст:

Hello from volume.

Первый контейнер был удалён:

`docker rm -f volume-test`

После этого был создан второй контейнер с тем же томом:

`docker run -dit --name volume-test-2 -v my-volume:/data ubuntu:latest bash`  
`docker exec volume-test-2 cat /data/test.txt`

Во втором контейнере сохранился файл с текстом `Hello from volume`. Это подтверждает, что данные в Docker Volume существуют отдельно от контейнеров.

После проверки второй контейнер был удалён:

`docker rm -f volume-test-2`

<img width="958" height="749" alt="image_2026-09-07_19-44-47" src="https://github.com/user-attachments/assets/36439b71-098c-47ed-ab3b-13b852ec6e06" />


*Рисунок 8 — создание тома, запись файла и проверка его сохранности во втором контейнере.*

## Результат

В ходе работы были выполнены следующие действия:

- проверена установка Docker;
- запущен тестовый контейнер `hello-world`;
- загружен и запущен образ `ubuntu:latest`;
- внутри контейнера Ubuntu установлен `curl`;
- запущен веб-сервер Nginx с пробросом порта `8080:80`;
- просмотрены логи Nginx и выполнено подключение к контейнеру;
- выполнены остановка, повторный запуск, удаление контейнера и удаление образа;
- создан Docker Volume и подтверждено сохранение данных после удаления контейнера.

## Вывод

В лабораторной работе изучены базовые операции Docker: работа с образами, контейнерами, пробросом портов, логами и именованными томами. Проверка с двумя контейнерами показала, что Docker Volume сохраняет данные после удаления контейнера.
