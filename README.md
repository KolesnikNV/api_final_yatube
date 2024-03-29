![Python](https://img.shields.io/badge/Python-blue?style=flat-square)
![Django](https://img.shields.io/badge/Django-green?style=flat-square)
![Django REST Framework](https://img.shields.io/badge/Django_REST_Framework-red?style=flat-square)
[![HTML](https://img.shields.io/badge/HTML-orange)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS](https://img.shields.io/badge/CSS-blueviolet)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![SQLite3](https://img.shields.io/badge/SQLite3-lightgrey)](https://www.sqlite.org/)
![Simple-JWT](https://img.shields.io/badge/Simple--JWT-yellow?style=flat-square)
![pytest](https://img.shields.io/badge/pytest-lightgrey?style=flat-square)


# api_final_yatube - REST API для проекта Yatube
# Установка:
Для начала необходимо клонировать репозиторий командой `git clone <ссылка на репозиторий>`
После прописать в консоли команду `cd api_final_yatube`
Далее необходимо установить зависимости командой `pip install -r requirements.txt`
После запустить сервер командой `python manage.py runserver` 

# Описание проекта

API доступен только аутентифицированным пользователям. В проекте аутентификация осуществляется по токену TokenAuthentication (Реализована аутентификация по JWT-токену).

Когда вы запустите проект, по адресу http://127.0.0.1:8000/redoc/ будет доступна документация для API Yatube. 
В документации описано, как как работает API. Документация представлена в формате Redoc.

Аутентифицированный пользователь авторизован на изменение и удаление своего контента; в остальных случаях доступ предоставляется только для чтения. **При попытке изменить чужие данные должен возвращаться код ответа `403 Forbidden`.**

Эндпоинты для взаимодействия с ресурсами:
  - api/v1/api-token-auth/ (POST): передаём логин и пароль, получаем токен.
  - api/v1/posts/ (GET, POST): получаем список всех постов или создаём новый пост.
  - api/v1/posts/{post_id}/ (GET, PUT, PATCH, DELETE): получаем, редактируем или удаляем пост по id.
  - api/v1/groups/ (GET): получаем список всех групп.
  - api/v1/groups/{group_id}/ (GET): получаем информацию о группе по id.
  - api/v1/posts/{post_id}/comments/ (GET, POST): получаем список всех комментариев поста с id=post_id или создаём новый, указав id поста, который хотим прокомментировать.
  - api/v1/posts/{post_id}/comments/{comment_id}/ (GET, PUT, PATCH, DELETE): получаем, редактируем или удаляем комментарий по id у поста с id=post_id.
  - api/v1/follow/ (GET): возвращает все подписки пользователя, сделавшего запрос. Возможен поиск по подпискам по параметру search.
  - api/v1/follow/ (POST): подписать пользователя, сделавшего запрос на пользователя, переданного в теле запроса.

В ответ на запросы **POST, PUT и PATCH** ваш API возвращает объект, который был добавлен или изменён.

# Примеры запросов

Пример POST-запроса с токеном Антона Чехова: добавление нового поста.
POST .../api/v1/posts/

{
    "text": "Тестовый текст для README.md."
} 

Пример ответа:

{
    "id": 1,
    "text": "Тестовый текст для README.md.",
    "author": "developer",
    "image": null,
    "group": 1,
    "pub_date": "2023-03-01T10:14:51.388932Z"
} 

Пример POST-запроса с токеном developer'а: отправляем новый комментарий к посту с id=1.
POST .../api/v1/posts/14/comments/

{
    "text": "Тест комментарий",
} 

Пример ответа:

{
    "id": 1,
    "author": "developer",
    "post": 14,
    "text": "Тест комментарий",
    "created": "2023-03-01T10:14:51.388932Z"
} 

Пример GET-запроса с токеном developer'а: получаем информацию о группе.
GET .../api/v1/groups/1/

Пример ответа:

{
    "id": 1,
    "title": "Python",
    "slug": "math",
    "description": "Посты на тему программирования"
} 
