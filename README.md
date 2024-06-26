# Kittygram_Docker
## Описание проекта:
Учебный проект KittyGram реализованный в сети контейнеров Docker cо сценарием запуска на удаленном сервере.
Социальная сеть для котиков с возможностью авторизации, публикации фотографий и достижений питомцев, управлением подписками на других пользователей.
#### Стек проекта: Python 3.9, Django 3.2.3, Django REST framework 3.12.4, JavaScript, Docker, Github Actions

## Структура и технические параметры проекта:

  - Весь проект состоит из контейнеров обьединенных в одну единую сеть.
   - Бекенд проекта расположен в контейнере kittygram_backend и привязан к порту 9000. 
    Работа этого контейнера не останавливается после запуска.
    Данный контейнер взаимодействует с контейнером БД и volumes: media и static

   - Фронтенд проекта расположен в контейнере kittygram_frontend, его задача при старте скопировать статику для запуска проекта
    и поместить ее в папку связанную с volume static. Затем остановить свою работу.

   - Контейнер Gateway перераспределяет запросы между остальными контейнерами. И является "входными воротами проекта".

   - Контейнер БД обрабатывает запросы при обращении к БД, работает в паре с контейнером бэкенда и volume: db

  - Файлы для обьединения контейнеров в сеть называются "COMPOSE":
   Данные файлы-инструкции описывают порядок и правила выполнения построения и обьединения контейнеров в единую сеть,
   иначе можно сказать отвечают за "ОРКЕСТРАЦИЮ" проекта. В проекте могут быть использованы несколько видов этих файлов:
    - Темплейт-файлы (Template files): Темплейт-файлы используются для создания динамических страниц или документов.
    - Продакшн-файлы (Production files): Продакшн-файлы представляют собой оптимизированные и готовые к развертыванию файлы, 
     которые используются в окружении реального проекта на боевом сервере или в продакшен.
    - Компоуз-файлы без суффикса: Это может быть общее название для файлов, которые не имеют конкретной роли или суффикса.
     Это файлы как правило необходимые в процессе разработки и для разработчиков.

  - Дополнительные файлы для запуска проекта:
    - Заполненный файл .env на основе файла .env.example(в корне проекта)
      Данный файл содержит список КОНСТАНТ необходимых для создания контейнеров и запуска проекта.


## Установка и запуск проекта:
- Клонировать репозиторий:
  ```
  git clone git@github.com:aten88/kittygram_docker.git
  ```
- В своем аккаунте на GitHub в разделе GitHub Actions Secrets передаем в КОНСТАНТЫ необходимые значения для запуска, в соответствии с примером .env.example:

- Константы для подключения к БД Postgres:
  POSTGRES_USER - администратор БД.
  POSTGRES_PASSWORD - пароль администратора БД.
  POSTGRES_DB - название БД.

- Константы Django:
  SECRET_KEY: - секретный ключ Django.
  ALLOWED_HOSTS: - список хостов для поключения.

- Переменные для доступа к DockerHub:
  username - логин.
  password - пароль.

- Переменные для подключению к серверу:
  host: - ip адрес сервера.
  username: - логин пользователя.
  key: - закрытый SSH ключ.
  passphrase: - пароль.

- Переменные для отчета в Telegram:
  to: - ID аккаунта Telegram.
  token: - Токен телеграмм-бота.

- Пушим проект в ветку main, ждем выполнения сценария, отчета в телеграмм об успешном выполнении, проверяем доступность проекта.

## Запуск проекта из исходников GitHub(локально):

- Клонируем репозиторий локально:
  ```
  git clone git@github.com:aten88/kittygram_docker.git
  ```
- Для того чтобы запустить проект(локально), вам необходимо создать и заполнить файл .env в корне проекта в соответствии с примером .env.example:
SECRET_KEY - секретный ключ Django. 
POSTGRES_DB - название БД. 
POSTGRES_USER - логин администратора БД. 
POSTGRES_PASSWORD - пароль администратора БД. 
DB_NAME - имя созданной в контейнере БД. 
DB_HOST - хост БД. 
DB_PORT - номер порта БД.

- Выполняем запуск:
  ```
  sudo docker compose -f docker-compose.yml up
  ```

- После запуска: Выполняем миграции и сбор статистики:
  ```
  sudo docker compose -f [имя-файла-docker-compose.yml] exec backend python manage.py migrate
  ```
  ```
  sudo docker compose -f [имя-файла-docker-compose.yml] exec backend python manage.py collectstatic
  ```
  ```
  sudo docker compose -f [имя-файла-docker-compose.yml] exec backend cp -r /app/collected_static/. /static/static/
  ```

- Проект доступен по адресу:
  ```
  http://localhost:9000/
  ```

- Остановка контейнеров:
В терминале, где был запуск, нажать Ctrl+С или в другом окне терминала:
   ```
   sudo docker compose -f docker-compose.yml down
   ```
 эта команда остановит и удалит все контейнеры и сети.

- Пример адреса в сети:
  ```
  https://aten-kittygramm.sytes.net/
  ```
### Автор: Алексей Тен.
