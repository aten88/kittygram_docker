Описание проекта
Социальная сеть для котов с возможностью публикации фотографий и их достижений.

Технологии которые применялись в данном проекте:
Python 3.9
Django 3.2.3
Django REST framework 3.12.4
JavaScript
Docker
Github Actions

Для запуска на сервере необходимо:

Склонировать репозиторий:
git clone git@github.com:aten88/kittygram_final.git

В своем аккаунте на GitHub в разделе GitHub Actions secrets заполняем константы для запуска(список констант имеется в файле main.yml)
Пушим проект в ветку main, ждем выполнения сценария и отчета в телеграмм об успешном выполнении.

Запуск проекта из исходников GitHub(локально)
Клонируем себе репозиторий:
git clone git@github.com:aten88/kittygram_final.git

Заполняем файл .env в соответствии с шаблоном .env.example

Выполняем запуск:
sudo docker compose -f docker-compose.yml up

После запуска: Миграции, сбор статистики
После запуска необходимо выполнить сбор статистики и миграции

sudo docker compose -f [имя-файла-docker-compose.yml] exec backend python manage.py migrate

sudo docker compose -f [имя-файла-docker-compose.yml] exec backend python manage.py collectstatic

sudo docker compose -f [имя-файла-docker-compose.yml] exec backend cp -r /app/collected_static/. /static/static/

И далее проект доступен на:
http://localhost:9000/

Остановка контейнеров
В терминале, где был запуск Ctrl+С или в другом окне: sudo docker compose -f docker-compose.yml down

Автор
Алексей Тен