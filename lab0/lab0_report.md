University: [ITMO University](https://itmo.ru/ru/)<br>
Faculty: [FTMI](https://ftmi.itmo.ru/)<br>
Course: [Введение в веб технологии](https://itmo-ict-faculty.github.io/introduction-in-web-tech/)<br>
Year: 2026/2027<br>
Group: U4225<br>
Author: Peshkov Andrey Konstantinovich<br>
Lab: Lab0<br>
Date of create: 04.09.2026<br>
Date of finished: 

# Лабораторная работа №0

## Создание репозитория и настройка рабочего окружения

## Ход работы

Проверена установка Git:

git --version

Получена версия:

Git version 2.53.0.windows.1.

Были настроены имя пользователя и электронная почта Git:

git config --global user.name "andrewwbbt"  
git config --global user.email "steam.peshkovcs@gmail.com"

Создан SSH-ключ типа ED25519 и добавлен в аккаунт GitHub. Подключение к GitHub успешно проверено командой:

ssh -T git@github.com

Получен ответ:

Hi andrewwbbt! You've successfully authenticated, but GitHub does not provide shell access.

Репозиторий был клонирован на компьютер:

git clone git@github.com:andrewwbbt/devops-lab-peshkov.git

Создана ветка для разработки:

git switch -c develop

В репозитории были подготовлены файлы README.md, .gitignore и CONTRIBUTING.md.

Изменения добавлены в индекс и сохранены коммитом:

git add .  
git commit -m "Initial project setup"

Ветка develop отправлена на GitHub:

git push -u origin develop

На GitHub был создан Pull Request из ветки develop в main. Pull Request был объединён с основной веткой, после чего ветка develop удалена.

## Результат

В результате работы:

- настроен Git;
- создан и подключён SSH-ключ;
- создан репозиторий GitHub devops-lab-peshkov;
- настроена работа с локальным репозиторием;
- создана ветка develop;
- выполнен коммит и отправка изменений на GitHub;
- создан и объединён Pull Request.
