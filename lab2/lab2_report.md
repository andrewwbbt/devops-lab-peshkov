University: [ITMO University](https://itmo.ru/ru/)<br>
Faculty: [FTMI](https://ftmi.itmo.ru/)<br>
Course: [Введение в веб технологии](https://itmo-ict-faculty.github.io/introduction-in-web-tech/)<br>
Year: 2025/2026<br>
Group: U4225<br>
Author: Peshkov Andrey Konstantinovich<br>
Lab: Lab2<br>
Date of create: 11.09.2026<br>
Date of finished:

# Лабораторная работа №2

## CI/CD для Docker-приложения

## Цель работы

Настроить CI/CD-пайплайн GitHub Actions для автоматической сборки Docker-образа, публикации в Docker Hub и выполнения шага деплоя при изменениях в ветке `main`.

## Ход работы

### 1. Подготовка Docker-приложения

В папке `lab2` подготовлено Flask-приложение со следующими файлами:

- `app.py` — приложение Flask, которое на запрос к маршруту `/` возвращает строку `Hello from Docker!`;
- `requirements.txt` — зависимости `Flask==2.0.1` и `Werkzeug==2.0.3`;
- `Dockerfile` — инструкция сборки образа на базе `python:3.9-slim`.

`Dockerfile` устанавливает `curl` и `vim`, копирует файлы приложения, создаёт пользователя `appuser` с UID 1000, открывает порт 5000 и запускает приложение командой `python app.py`.

### 2. Создание репозитория Docker Hub

Создан публичный Docker Hub-репозиторий `andrewwbbt/devops-lab`.
<img width="904" height="461" alt="image" src="https://github.com/user-attachments/assets/b6c84275-1b18-4570-9f31-b3e68b2e9da0" />

*Рисунок 1 — создание публичного Docker Hub-репозитория `devops-lab`.*

### 3. Настройка секретов GitHub

В настройках GitHub-репозитория созданы секреты для авторизации в Docker Hub:

- `DOCKER_USERNAME` — логин Docker Hub;
- `DOCKER_PASSWORD` — Docker Hub Personal Access Token с правами Read & Write.

Значения секретов не хранятся в коде и не отображаются в отчёте. Успешное выполнение шага авторизации в workflow подтверждает правильность их настройки.

<img width="1067" height="767" alt="image" src="https://github.com/user-attachments/assets/465d326e-d140-475c-9628-36932e235c12" />

*Рисунок 2 — настроенные секреты GitHub Actions без отображения их значений.*

### 4. Настройка GitHub Actions

В корне репозитория создан workflow `.github/workflows/docker-build.yml`.

Workflow запускается при каждом push в ветку `main`. Он использует GitHub-hosted runner `ubuntu-latest` и выполняет следующие этапы:

1. Checkout кода репозитория.
2. Настройка Docker Buildx.
3. Авторизация в Docker Hub через `DOCKER_USERNAME` и `DOCKER_PASSWORD`.
4. Сборка образа из контекста `./lab2` и файла `./lab2/Dockerfile`.
5. Публикация образа в Docker Hub с тегом `andrewwbbt/devops-lab:latest`.
6. Выполнение шага деплоя с сообщением `Deploy step completed`.
<img width="741" height="757" alt="image" src="https://github.com/user-attachments/assets/85379499-91dc-4f7c-9728-05fb5b9d2377" />

*Рисунок 3 — конфигурация workflow GitHub Actions.*

<img width="240" height="339" alt="image" src="https://github.com/user-attachments/assets/121255b3-dfd1-41ab-84a1-0becfd4a4a8e" />

*Рисунок 4 — структура репозитория с workflow и исходными файлами приложения.*

### 5. Тестирование pipeline

После добавления файлов приложения в ветку `main` GitHub Actions автоматически запустил workflow `Build and Push Docker Image`.

Первые запуски завершились ошибкой, потому что файлы приложения добавлялись отдельными коммитами и контекст ./lab2 был неполным. После добавления всех файлов выполнен итоговый успешный запуск.
Итоговый запуск завершился успешно. Все этапы получили статус success:

- `Checkout code`;
- `Set up Docker Buildx`;
- `Log in to Docker Hub`;
- `Build and push Docker image`;
- `Deploy`.

<img width="1098" height="756" alt="image" src="https://github.com/user-attachments/assets/e120faa8-17a8-41b5-8d87-d02fcca95898" />

*Рисунок 5 — успешное выполнение CI/CD-пайплайна GitHub Actions.*

### 6. Проверка публикации образа

В Docker Hub-репозитории `andrewwbbt/devops-lab` появился образ с тегом `latest`. Время публикации соответствует времени успешного запуска GitHub Actions.

<img width="1213" height="525" alt="image" src="https://github.com/user-attachments/assets/157023f6-6bf5-4f9c-b434-fc691c73a0a7" />

*Рисунок 7 — опубликованный Docker-образ `andrewwbbt/devops-lab:latest`.*

## Результат

В ходе работы был создан CI/CD-пайплайн GitHub Actions. При push в ветку `main` он автоматически получает исходный код, настраивает Docker Buildx, авторизуется в Docker Hub, собирает образ Flask-приложения и публикует его с тегом `latest`. После публикации выполняется предусмотренный заданием шаг деплоя. Я настроил автоматическую сборку и публикацию Docker-образа через GitHub Actions. Секреты Docker Hub не размещены в исходном коде, а используются только в настройках репозитория. Успешное выполнение workflow и наличие тега `latest` в Docker Hub подтверждают работоспособность pipeline.


