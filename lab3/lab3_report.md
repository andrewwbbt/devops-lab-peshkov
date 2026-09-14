University: [ITMO University](https://itmo.ru/ru/)<br>
Faculty: [FTMI](https://ftmi.itmo.ru/)<br>
Course: [Введение в веб технологии](https://itmo-ict-faculty.github.io/introduction-in-web-tech/)<br>
Year: 2026/2027<br>
Group: U4225<br>
Author: Peshkov Andrey Konstantinovich<br>
Lab: Lab3<br>
Date of create: 14.09.2026<br>
Date of finished: 

# Лабораторная работа №3

## Мониторинг с Prometheus и Grafana

## Цель работы

Настроить локальную систему мониторинга на основе Prometheus, Node Exporter и Grafana; собрать системные метрики и визуализировать их на дашборде.

## Ход работы

### 1. Подготовка конфигурации Prometheus

В репозитории была создана папка lab3, а в ней папка prometheus. В файле prometheus/prometheus.yml задан интервал сбора метрик 15 секунд.

В конфигурации добавлены две задачи сбора метрик:

- prometheus — сбор метрик самого Prometheus по адресу prometheus:9090;
- node-exporter — сбор системных метрик по адресу node-exporter:9100.

<img width="780" height="578" alt="photo_1_2026-09-14_15-42-32" src="https://github.com/user-attachments/assets/ba44d62c-7070-4a72-8e1f-e0efafde31a7" />

*Рисунок 1 — создание структуры папок и конфигурация prometheus.yml.*

### 2. Запуск Node Exporter

Для связи контейнеров была создана Docker-сеть monitoring. Затем был запущен контейнер node-exporter, подключённый к этой сети. Для контейнера опубликован порт 9100, а также подключены системные каталоги /proc, /sys и / в режиме только для чтения.

Работа Node Exporter проверена запросом:

curl http://localhost:9100/metrics

В ответ получен список метрик. Это подтверждает, что Node Exporter собирает и отдаёт данные по HTTP.

<img width="970" height="986" alt="photo_2_2026-09-14_15-42-32" src="https://github.com/user-attachments/assets/38fa3be4-0b55-4efe-9070-306ac6b28a45" />

*Рисунок 2 — запуск Node Exporter и получение метрик через HTTP.*

### 3. Запуск Prometheus

Для хранения данных Prometheus создан именованный том prometheus-data. Контейнер Prometheus был подключён к сети monitoring, а конфигурация prometheus.yml смонтирована в каталог /etc/prometheus контейнера.

После запуска Prometheus была открыта страница Status → Target health. Оба target имеют статус UP:

- prometheus;
- node-exporter.

Это подтверждает, что Prometheus успешно получает метрики от Node Exporter.

<img width="1280" height="300" alt="photo_3_2026-09-14_15-42-32" src="https://github.com/user-attachments/assets/d2d7e831-03b0-42ad-8c89-6c1956532ebe" />

*Рисунок 3 — статусы target Prometheus: prometheus и node-exporter доступны.*

### 4. Запуск Grafana

Для хранения данных Grafana создан именованный том grafana-data. Контейнер Grafana подключён к сети monitoring и опубликован на порту 3000.

Проверка команды docker ps показала, что контейнеры grafana, prometheus и node-exporter находятся в состоянии Up.

<img width="966" height="175" alt="photo_4_2026-09-14_15-42-32" src="https://github.com/user-attachments/assets/685dafaf-4dda-48c2-b44e-a98dcfcdd135" />

*Рисунок 4 — работающие контейнеры Grafana, Prometheus и Node Exporter.*

Grafana была открыта по адресу http://localhost:3000. Выполнен вход под учётной записью администратора.

<img width="868" height="797" alt="photo_5_2026-09-14_15-42-32" src="https://github.com/user-attachments/assets/efc3c161-8e13-4bab-928f-c282714535c5" />

*Рисунок 5 — форма входа в Grafana.*

### 5. Подключение Prometheus в Grafana

В Grafana добавлен источник данных Prometheus. В качестве URL указан адрес http://prometheus:9090. Этот адрес используется внутри Docker-сети monitoring: Grafana находит контейнер Prometheus по его имени.

<img width="1280" height="616" alt="photo_7_2026-09-14_15-42-32" src="https://github.com/user-attachments/assets/249de8f2-d29f-49f4-a46b-79c64f714fb7" />

*Рисунок 6 — настройка источника данных Prometheus в Grafana.*

После сохранения Grafana успешно выполнила запрос к Prometheus API.

<img width="872" height="144" alt="photo_6_2026-09-14_15-42-32" src="https://github.com/user-attachments/assets/a8c6e47e-98a7-4692-a936-511af53bd678" />

*Рисунок 7 — успешная проверка подключения Grafana к Prometheus.*

### 6. Создание дашборда

Для проверки исходной метрики CPU в Grafana была выбрана метрика node_cpu_seconds_total. Эта метрика содержит значения для каждого ядра и режима работы процессора.

<img width="1280" height="950" alt="photo_8_2026-09-14_15-42-32" src="https://github.com/user-attachments/assets/4553f490-29b5-4a4b-a8b8-63b0ed4af964" />

*Рисунок 8 — выбор метрики node_cpu_seconds_total в Grafana.*

Для удобного отображения был создан дашборд с отдельными панелями:

- Использование CPU — процент загрузки процессора, рассчитанный на основе node_cpu_seconds_total;
- Память — процент использования оперативной памяти;
- Использование диска — процент занятого дискового пространства.

<img width="1280" height="564" alt="photo_9_2026-09-14_15-42-32" src="https://github.com/user-attachments/assets/9565ce7f-6724-4092-bc00-088897008103" />

*Рисунок 9 — дашборд Grafana с графиками CPU, памяти и диска.*

## Результат

В ходе работы настроена система мониторинга из трёх Docker-контейнеров. Node Exporter собирает системные метрики, Prometheus запрашивает их с интервалом 15 секунд и хранит результаты, а Grafana получает данные из Prometheus и отображает их на дашборде.
