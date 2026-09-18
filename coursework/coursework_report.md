University: [ITMO University](https://itmo.ru/ru/)<br>
Faculty: FTMI<br>
Course: [Введение в веб технологии](https://itmo-ict-faculty.github.io/introduction-in-web-tech/)<br>
Year: 2026/2027<br>
Group: U4225<br>
Author: Peshkov Andrey Konstantinovich<br>
Work: Coursework<br>
Date of create: 14.09.2026<br>
Date of finished:

# Курсовая работа

## Создание персонального сайта с использованием MkDocs

## Цель работы

Создать персональный сайт на основе MkDocs и Markdown, настроить тему Material, структуру навигации, поиск, стилизацию и автоматическую публикацию через GitHub Pages.

## Используемые технологии

В работе использовались Python, MkDocs, тема Material for MkDocs, Markdown, CSS, Git, GitHub, GitHub Actions и GitHub Pages.

## 1. Подготовка среды и создание проекта

Для работы были установлены MkDocs и тема Material. После проверки версии MkDocs был создан начальный проект. На первом этапе рабочая папка называлась `lab4`; после завершения настройки она была переименована в `coursework`, так как сайт является курсовой работой.

<img width="979" height="632" alt="photo_2026-09-14_23-24-54" src="https://github.com/user-attachments/assets/dc94c7c2-7b16-422e-84fb-be6114fa3533" />

*Рисунок 1 — установка MkDocs Material, проверка версии и создание начального проекта.*

В результате инициализации были созданы файл `mkdocs.yml` и папка `docs` с главной страницей сайта.

## 2. Структура и конфигурация сайта

Итоговая структура проекта расположена в папке `coursework`. В ней находятся конфигурационный файл `mkdocs.yml`, исходные Markdown-страницы в папке `docs`, изображения и таблица стилей.

```text
coursework/
├── docs/
│   ├── images/
│   │   └── logo.png
│   ├── stylesheets/
│   │   └── extra.css
│   ├── index.md
│   ├── about.md
│   ├── projects.md
│   ├── contacts.md
│   ├── achievements.md
│   └── resume.md
└── mkdocs.yml
```

На раннем этапе в конфигурации были заданы основные параметры сайта, тема Material, поиск и навигация.

<img width="775" height="878" alt="photo_2026-09-14_23-25-52" src="https://github.com/user-attachments/assets/81dc6083-fd93-419d-ba37-e32c71fd2911" />

*Рисунок 2 — первоначальная настройка файла mkdocs.yml.*

<img width="698" height="228" alt="photo_2026-09-14_23-40-49" src="https://github.com/user-attachments/assets/8a214623-64ed-48f9-9f37-8f62bf59e822" />

*Рисунок 3 — первоначальная структура страниц в папке docs.*

В финальном `mkdocs.yml` указаны название, описание, автор и URL сайта. Настроены тема Material, фиолетовая палитра `slate`, цвета `deep purple` и `pink`, расширения Markdown, поиск, навигация и ссылки на социальные сети. Логотип подключён как логотип и фавикон сайта.

<img width="774" height="938" alt="image" src="https://github.com/user-attachments/assets/c32b8961-2f73-4567-95c0-e4a6e4cc78be" />

*Рисунок 4 — итоговая конфигурация MkDocs-сайта.*

## 3. Создание страниц и контента

Главная страница содержит краткую информацию об авторе, логотип, кнопки перехода и навигационные карточки. Карточки ведут на страницы «О себе», «Проекты» и «Контакты».

Страница «О себе» содержит сведения об образовании, список навыков, список интересов и таблицу уровней навыков. На странице «Проекты» размещены три проекта: исследовательская работа по оценке крипто-стартапов, проект SVADLY и учебный DevOps-проект. Каждый проект оформлен отдельной карточкой. Страница контактов содержит ссылки на GitHub, Telegram и адрес электронной почты. Дополнительно созданы страницы достижений и резюме.

На страницах использованы заголовки, маркированные и нумерованные списки, ссылки, изображение логотипа, цитата, таблица и HTML-блоки с CSS-классами для карточек.

<img width="2269" height="1314" alt="image" src="https://github.com/user-attachments/assets/60f85128-085b-4ce5-baee-8aff3cfda00e" />

*Рисунок 5 — главная страница опубликованного сайта.*

<img width="2091" height="1314" alt="image" src="https://github.com/user-attachments/assets/a9f78e1f-c0e4-4651-ab33-a9de6bc782d2" />

*Рисунок 6 — страница «О себе» с таблицей навыков.*

<img width="1759" height="1260" alt="image" src="https://github.com/user-attachments/assets/efa85c16-1a96-4c46-9716-9a0126c25dda" />

*Рисунок 7 — страница проектов с карточками.*

## 4. Стилизация и дополнительные возможности

Для сайта создана дополнительная таблица стилей `docs/stylesheets/extra.css`. Она задаёт тёмный фон, фиолетовую шапку с градиентом, оформление карточек, таблиц и кнопок. Логотип увеличен с помощью CSS без изменения высоты шапки.

В конфигурации включён плагин поиска. Он создаёт поисковый индекс при сборке сайта и позволяет искать материалы по словам, например `Docker` или `SVADLY`.

<img width="1979" height="1228" alt="image" src="https://github.com/user-attachments/assets/dd6b784f-78ed-48f4-b6a4-6b9ad1a30ed3" />

*Рисунок 8 — поиск по материалам сайта.*

## 5. Локальное тестирование

Перед публикацией сайт был собран командой `py -m mkdocs build --strict`. В результате создана папка `coursework/site` со статическими HTML-, CSS- и JavaScript-файлами. Папка сборки добавлена в `.gitignore` и не отправляется в репозиторий.

<img width="898" height="428" alt="image" src="https://github.com/user-attachments/assets/edc0d0de-2089-42e9-bcef-4e0914c92227" />

*Рисунок 9 — успешная локальная сборка сайта MkDocs.*

## 6. Автоматическая публикация через GitHub Pages

Для автоматической публикации создан workflow `.github/workflows/deploy-mkdocs.yml`. При push в ветку `main` workflow устанавливает тему Material, собирает сайт из папки `coursework`, загружает папку `coursework/site` как артефакт и развёртывает её в GitHub Pages.

В настройках репозитория в разделе Settings → Pages выбран источник публикации GitHub Actions. Workflow успешно выполнил этапы `build` и `deploy`.

<img width="1075" height="656" alt="image" src="https://github.com/user-attachments/assets/51e72383-292a-4bed-936f-992d7904a194" />

*Рисунок 11 — настройка GitHub Pages для публикации через GitHub Actions.*

<img width="2074" height="1004" alt="image" src="https://github.com/user-attachments/assets/252895da-8ebc-4347-85b3-29fc595cc0dd" />

*Рисунок 12 — успешная сборка и публикация сайта через GitHub Actions.*

После завершения workflow сайт опубликован по адресу [https://andrewwbbt.github.io/devops-lab-peshkov/](https://andrewwbbt.github.io/devops-lab-peshkov/).

## Результат

Создан персональный сайт на MkDocs с темой Material. На сайте настроены навигация, поиск, логотип, фиолетовая цветовая схема и дополнительные стили. Созданы страницы с информацией об авторе, проектах, контактах, достижениях и резюме. Сайт успешно собирается локально и автоматически публикуется через GitHub Actions на GitHub Pages.
