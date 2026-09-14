University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Введение в веб технологии](https://itmo-ict-faculty.github.io/introduction-in-web-tech/)  
Year: 2026/2027  
Group: U4225  
Author: Davidyan Milana Eduardovnа  
Lab: Lab0  
Date of create: 13.09.2026  
Date of finished: 

# Лабораторная работа №2

## CI/CD для Docker приложения

### Ход работы

Для выполнения лабораторной работы был создан отдельный репозиторий на GitHub:

```text
docker-ci-cd-davidyan
```

Также был создан репозиторий на Docker Hub:

```text
miladavidyan/my-flask-app
```

## Подготовка проекта

В GitHub-репозитории были созданы файлы приложения:

```text
app.py
requirements.txt
Dockerfile
```

Файл `app.py` содержит простое Flask-приложение, которое запускается на порту `5000`.

Файл `requirements.txt` содержит зависимость:

```text
Flask==2.0.1
```

В `Dockerfile` была настроена сборка Docker-образа на основе Python.

## Настройка GitHub Actions

В корне репозитория была создана директория:

```text
.github/workflows/
```

В ней был создан файл:

```text
docker-build.yml
```

Для пайплайна была настроена автоматическая активация при push в ветку `main`:

```yaml
on:
  push:
    branches:
      - main
```

Для выполнения workflow используется runner:

```yaml
runs-on: ubuntu-latest
```

В пайплайн были добавлены следующие этапы:

- получение кода из GitHub-репозитория;
- настройка Docker Buildx;
- авторизация в Docker Hub;
- сборка Docker-образа;
- публикация образа в Docker Hub;
- выполнение шага деплоя.

Для получения кода использовался:

```yaml
uses: actions/checkout@v4
```

Для настройки Docker Buildx:

```yaml
uses: docker/setup-buildx-action@v3
```

Для входа в Docker Hub:

```yaml
uses: docker/login-action@v3
```

Сборка и публикация образа выполнялись с помощью:

```yaml
uses: docker/build-push-action@v6
```

Образ публиковался с тегом:

```text
miladavidyan/my-flask-app:latest
```

Для шага деплоя было добавлено сообщение:

```yaml
run: echo "Deploying application..."
```

## Настройка секретов

В настройках GitHub-репозитория были созданы секреты:

```text
DOCKER_USERNAME
DOCKER_PASSWORD
```

В `DOCKER_USERNAME` был указан логин Docker Hub.

В `DOCKER_PASSWORD` был сохранён Personal Access Token, созданный в Docker Hub.

Секреты использовались в workflow:

```yaml
username: ${{ secrets.DOCKER_USERNAME }}
password: ${{ secrets.DOCKER_PASSWORD }}
```

Это позволило не хранить данные для авторизации непосредственно в коде репозитория.

## Тестирование пайплайна

После внесения изменений в ветку `main` GitHub Actions автоматически запустил workflow.

В разделе `Actions` было проверено успешное выполнение всех этапов:

```text
Checkout repository
Set up Docker Buildx
Login to Docker Hub
Build and push Docker image
Deploy
```

Все этапы завершились успешно.

После выполнения workflow в Docker Hub появился Docker-образ:

```text
miladavidyan/my-flask-app
```

с тегом:

```text
latest
```

Для дополнительной проверки пайплайна в репозитории было сделано новое изменение и создан новый коммит в ветке `main`.

После этого GitHub Actions снова автоматически запустил пайплайн, а время публикации тега `latest` в Docker Hub обновилось.

Таким образом была подтверждена автоматическая сборка и публикация Docker-образа при изменениях в ветке `main`.

## Вывод

В ходе лабораторной работы был настроен CI/CD пайплайн с использованием GitHub Actions.

Была реализована автоматическая сборка Docker-образа, авторизация в Docker Hub с использованием секретов и автоматическая публикация образа в registry.

Также было проверено автоматическое выполнение пайплайна после изменений в ветке `main`.

Дополнительное задание со звёздочкой не выполнялось.

<img width="578" height="242" alt="image" src="https://github.com/user-attachments/assets/7cb18943-a8b2-496b-b2ec-c8f8d35ec33f" />
<img width="1060" height="448" alt="image" src="https://github.com/user-attachments/assets/f1e688ba-e7eb-43ec-84d3-99b744be5a26" />
<img width="625" height="230" alt="image" src="https://github.com/user-attachments/assets/25fc4def-662e-463d-8c80-eb791bb25d47" />
<img width="663" height="439" alt="image" src="https://github.com/user-attachments/assets/fdfb1de0-de85-4c1f-8c9f-0d084efa538f" />
<img width="920" height="812" alt="image" src="https://github.com/user-attachments/assets/66f1e418-4433-41c0-b389-69198c319016" />
<img width="639" height="469" alt="image" src="https://github.com/user-attachments/assets/ad02c8ca-fd17-43ea-b4c3-59e6aa126239" />
<img width="628" height="532" alt="image" src="https://github.com/user-attachments/assets/2d2ca0c6-3a56-470c-a691-b92ec52d4e08" />
<img width="904" height="719" alt="image" src="https://github.com/user-attachments/assets/ba25e68b-a206-4a21-9ab0-b898dd51ec38" />
