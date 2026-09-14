University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Введение в веб технологии](https://itmo-ict-faculty.github.io/introduction-in-web-tech/)  
Year: 2026/2027  
Group: U4225  
Author: Davidyan Milana Eduardovnа  
Lab: Lab0  
Date of create: 13.09.2026  
Date of finished: 
# Лабораторная работа №1

## Основы работы с Docker

### Ход работы

Был установлен Docker Desktop для Windows.

Установка Docker была проверена командой:

```powershell
docker --version
```

Для проверки корректной работы Docker был запущен тестовый контейнер:

```powershell
docker run hello-world
```

В результате было получено сообщение:

```text
Hello from Docker!
```

Также были изучены базовые команды:

```powershell
docker images
docker ps
docker ps -a
```

## Работа с образом Ubuntu

Был скачан образ Ubuntu:

```powershell
docker pull ubuntu:latest
```

После этого был запущен интерактивный контейнер:

```powershell
docker run -it ubuntu bash
```

Внутри контейнера были обновлены списки пакетов:

```bash
apt update
```

Затем был установлен пакет `curl`:

```bash
apt install -y curl
```

Установка была проверена командой:

```bash
curl --version
```

После завершения работы был выполнен выход из контейнера:

```bash
exit
```

## Запуск веб-сервера nginx

Был запущен контейнер nginx:

```powershell
docker run -d -p 8080:80 --name web-server nginx:alpine
```

Работа веб-сервера была проверена в браузере по адресу:

```text
http://localhost:8080
```

Также были просмотрены логи контейнера:

```powershell
docker logs web-server
```

Для подключения к контейнеру была использована команда:

```powershell
docker exec -it web-server sh
```

## Управление контейнерами

Были изучены команды для просмотра контейнеров:

```powershell
docker ps
docker ps -a
```

Контейнер `web-server` был остановлен:

```powershell
docker stop web-server
```

После этого контейнер был снова запущен:

```powershell
docker start web-server
```

Затем контейнер был остановлен и удалён:

```powershell
docker stop web-server
docker rm web-server
```

Образ nginx также был удалён:

```powershell
docker rmi nginx:alpine
```

## Работа с Docker volumes

Был создан том:

```powershell
docker volume create my-volume
```

Контейнер был запущен с подключённым томом:

```powershell
docker run -it --name volume-test -d -v my-volume:/data ubuntu bash
```

В томе был создан файл:

```powershell
docker exec volume-test sh -c "echo 'Hello from volume' > /data/test.txt"
```

Содержимое файла было проверено:

```powershell
docker exec volume-test cat /data/test.txt
```

После этого контейнер был удалён, а новый контейнер был создан с тем же томом:

```powershell
docker stop volume-test
docker rm volume-test
docker run -d --name volume-test-2 -v my-volume:/data ubuntu sleep infinity
```

Содержимое файла было проверено повторно:

```powershell
docker exec volume-test-2 cat /data/test.txt
```

В результате снова было получено:

```text
Hello from volume
```

Это подтвердило, что данные в Docker volume сохраняются независимо от жизненного цикла контейнера.

## Вывод

В ходе лабораторной работы были изучены основы работы с Docker.

Были выполнены установка и настройка Docker Desktop, работа с образами и контейнерами, запуск nginx, управление контейнерами и работа с Docker volumes.

Дополнительное задание со звёздочкой не выполнялось.

### Скриншоты выполнения

<img width="671" height="509" alt="image" src="https://github.com/user-attachments/assets/e7052ff3-0a0a-4e90-9bcb-4e8d7f03ff87" />
<img width="1520" height="105" alt="image" src="https://github.com/user-attachments/assets/0e37c70c-45ef-4237-baa2-eb931f6be5bb" />
<img width="915" height="122" alt="image" src="https://github.com/user-attachments/assets/b1a512db-381e-4936-8889-07451276b759" />
<img width="714" height="186" alt="image" src="https://github.com/user-attachments/assets/302dd331-2b92-4bcb-8604-42e886d18306" />
<img width="794" height="439" alt="image" src="https://github.com/user-attachments/assets/38498f5f-fe17-4ad2-bc7c-9a1f6a7509dd" />
<img width="1692" height="95" alt="image" src="https://github.com/user-attachments/assets/63a37c6b-dd26-475b-a414-aba83dcd9f10" />
<img width="677" height="293" alt="image" src="https://github.com/user-attachments/assets/71baed80-9d6c-437d-8dd9-55d640596d91" />
<img width="1362" height="468" alt="image" src="https://github.com/user-attachments/assets/77d21dc9-cbce-479a-9931-20550dd8502f" />
<img width="1886" height="837" alt="image" src="https://github.com/user-attachments/assets/a4385794-f1ca-47d2-b693-c94e6f632c63" />
<img width="962" height="725" alt="image" src="https://github.com/user-attachments/assets/b93dae7a-0a74-4f61-b289-8da507d2b45e" />
<img width="686" height="156" alt="image" src="https://github.com/user-attachments/assets/ea04cd5b-54ac-43bf-80b8-da1562999545" />
<img width="820" height="174" alt="image" src="https://github.com/user-attachments/assets/4fee0d6b-e374-4983-ba7b-6db2cf7016c8" />
<img width="559" height="46" alt="image" src="https://github.com/user-attachments/assets/52aaea96-e087-4066-8035-07d487c4101c" />
