﻿
![example workflow](https://github.com/4kolesov/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)


### REST API для YaMdB!!!!!
Ссылка — http://ynx69.hopto.org
Документация: http://ynx69.hopto.org/redoc/
### Возможности:
Проект YaMDb собирает отзывы пользователей на произведения. Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

Произведения делятся на категории, такие как «Книги», «Фильмы», «Музыка». Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Жуки» и вторая сюита Баха. Список категорий может быть расширен (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).

Произведению может быть присвоен жанр из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»).

Добавлять произведения, категории и жанры может только администратор.
Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.

Добавлять отзывы, комментарии и ставить оценки могут только аутентифицированные пользователи.

### Шаблон заполнения файла .env с переменными окружения для работы с базой данных:

    DB_NAME= # имя базы данных
    POSTGRES_USER= # логин для подключения к базе данных
    POSTGRES_PASSWORD= # пароль для подключения к БД (установите свой)
    DB_HOST= # название сервиса (контейнера)
    DB_PORT= # порт для подключения к БД


### Для запуска проекта в Docker:

1. Загрузить образ проекта: `docker push 4kolesov/api_yamdb`
2. Запустить контейнер `docker run api_yamdb`
3. Выполнить по очереди команды:
`docker-compose exec web python manage.py migrate`
`docker-compose exec web python manage.py createsuperuser`
`docker-compose exec web python manage.py collectstatic --no-input`
4. Для тестового заполнения базы данных необходимо ввести команду `docker-compose exec web python manage.py loaddata db.json`

### Для создания собственного контейнера Docker:
1. Скачать и распаковать все [файлы](https://github.com/4kolesov/infra_sp2 "файлы")
2. Запустить терминал Bash, перейти в папку /infra/
3.  Запускаем команду `docker-compose up`
4. Выполнить по очереди команды:
`docker-compose exec web python manage.py migrate`
`docker-compose exec web python manage.py createsuperuser`
`docker-compose exec web python manage.py collectstatic --no-input`
5. Для тестового заполнения базы данных необходимо ввести команду `docker-compose exec web python manage.py loaddata db.json`

### Для загрузки данных из .csv файлов необходимо:
• расположить файлы в папке статики: /data

• запустить менеджер команду loadcsv из директории с файлом manage.py
`docker-compose exec web python manage.py loadcsv`
если добавить аргумент `—clear_base` — будут очищены таблицы перед записью
если добавить аргумент `—only_err_msg` — в терминал будет выводить только основные сообщения и сообщения об ошибках
`docker-compose exec web python manage.py loadcsv --clear_base --only_err_msg`




### Авторы проекта:
Мария Постолова — Отзывы, Комментарии, эндпоинты, разрешения.

Рабадан Ибрагимов — Категории, Жанры, Произведения, импорт из CSV в БД, Рейтинг Произведений, эндпоинты, разрешения.

Александр Колесов — Регистрация и аутентификация пользователей, Роли, подтверждение через Email, выдача токена, эндпоинты, разрешения, контейнеризация в Docker Compose, размещение контейнера на Яндекс.Облаке, внедрение GitHub Actions.
