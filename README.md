# Домашнее задание к занятию 4 «Оркестрация группой Docker контейнеров на примере Docker Compose»

## Задача 1
- ...
- Предоставьте ответ в виде ссылки на https://hub.docker.com/<username_repo>/custom-nginx/general. - https://hub.docker.com/repository/docker/hawk0775/custom-nginx/general

## Задача 2
1. Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
- имя контейнера "ФИО-custom-nginx-t2"
- контейнер работает в фоне
- контейнер опубликован на порту хост системы 127.0.0.1:8080
2. Не удаляя, переименуйте контейнер в "custom-nginx-t2"
3. Выполните команду ```date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html```
4. Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

![alt text](https://raw.githubusercontent.com/hawk0774/05-virt-03-docker-compose/main/Screenshot_5.png)

![alt text](https://raw.githubusercontent.com/hawk0774/05-virt-03-docker-compose/main/Screenshot_6.png)

![alt text](https://raw.githubusercontent.com/hawk0774/05-virt-03-docker-compose/main/Screenshot_7.png)

## Задача 3
1. Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
- Для подключения к стандартному потоку ввода-вывода требется выполнить команду docker attach. При нажатии комбинации Ctrl-C контейнер остановится так как это отправляет сигнал прерывания (SIGINT) процессу внутри контейнера, процесс завершается и следовательно завершает работу контейнер.

![alt text](https://raw.githubusercontent.com/hawk0774/05-virt-03-docker-compose/main/Screenshot_1.png)

4. Перезапустите контейнер
5. Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.
6. Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.
![alt text](https://raw.githubusercontent.com/hawk0774/05-virt-03-docker-compose/main/Screenshot_2.png) 
8. Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".
![alt text](https://raw.githubusercontent.com/hawk0774/05-virt-03-docker-compose/main/Screenshot_3.png)
9. Запомните(!) и выполните команду ```nginx -s reload```, а затем внутри контейнера ```curl http://127.0.0.1:80 ; curl http://127.0.0.1:81```.

![alt text](https://raw.githubusercontent.com/hawk0774/05-virt-03-docker-compose/main/Screenshot_4.png)
![alt text](https://raw.githubusercontent.com/hawk0774/05-virt-03-docker-compose/main/Screenshot_8.png)

10. Выйдите из контейнера, набрав в консоли  ```exit``` или Ctrl-D.
11. Проверьте вывод команд: ```ss -tlpn | grep 127.0.0.1:8080``` , ```docker port custom-nginx-t2```, ```curl http://127.0.0.1:8080```. Кратко объясните суть возникшей проблемы.
- Порт 8080 custom-nginx-t2 остался открытым, но он прибинден к порту 80 внутри контейнера, а так как nginx перестал прослушивать порт 80, то сетевой доступ пропал. 
![alt text](https://raw.githubusercontent.com/hawk0774/05-virt-03-docker-compose/main/Screenshot_9.png)
