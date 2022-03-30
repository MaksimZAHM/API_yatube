# Проект «API для Yatube»

>Учебный проект в рамках курса __Python-developer__ на платформе __Яндекс.Практикум__

## Описание
API для приложения [Yatube](https://github.com/MaksimZAHM/Yatube) - социальной сети для чтения и публикации постов и комментариев к ним.

Реализован REST API CRUD для основных моделей проекта, для аутентификации примненяется JWT-токен. В проекте реализованы пермишены, фильтрации, сортировки и поиск по запросам клиентов, реализована пагинация ответов от API, установлено ограничение количества запросов к API.

## Системные требования
- Python 3.7+
- Works on Linux, Windows, macOS

## Стек технологий:
- Python 3.7
- Django 3.2
- Django RESTFramework
- Simple-JWT

## API для сервиса __Yatube__ позволяет:
* работать с публикациями:
  * получать список всех публикаций
  * создавать (обновлять, удалять) публикации

* работать с комментариями к публикациям:
  * добавлять (получать, обновлять, удалять) комментарии

* Получать список сообществ
* Подписываться на пользователей
* Получать и обновлять JWT-токены

__Ознакомиться с полным функционалом и примерами можно по адресу__   
__http://127.0.0.1:8000/redoc__  
__( Доступно после запуска проекта )__

## Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:
```
git clone ссылка на репозиторий
cd API_yatube
```

Cоздать и активировать виртуальное окружение:
```
python3 -m venv venv
source venv/Scripts/activate
```

Установить зависимости из файла requirements.txt:
```
pip install -r requirements.txt
```

Перейти в каталог с manage.py
```
cd yatube_api
```

Выполнить миграции:
```
python3 manage.py migrate
```

Запустить проект:
```
python3 manage.py runserver
```

## Примеры работы с API
API Yatube возвращает ответы в формате JSON.

__GET-запрос__ на получение списка публикаций или публикации по id:

```
http://127.0.0.1:8000/api/v1/posts/  

http://127.0.0.1:8000/api/v1/posts/{id}/
```

```
Ответ:
{
  "id": 1,
  "text": "Новый пост",
  "author": "admin",
  "group": null,
  "image": null,
  "pub_date": "2022-01-03T10:00:39.364506Z",
  "comments": []
}
```
__GET-запрос__ на получение списка всех публикаций с указанием параметров __limit__ и __offset__:

 > __limit__ - какое число объектов вернётся

 > __offset__ - с какого по счёту объекта начнется отсчёт

```
http://127.0.0.1:8000/api/v1/posts/?limit=2&offset=2
```

API возвращает список с пагинацией:

```
Ответ:
{
  "count": 4,
  "next": null,
  "previous": "http://127.0.0.1:8000/api/v1/posts/?limit=2",
  "results": [
    {
      "id": 3,
      "text": "И еще один новый пост",
      "author": "admin",
      "group": null,
      "image": null,
      "pub_date": "2022-01-05T08:44:55.037434Z",
      "comments": []
    },
    {
      "id": 4,
      "text": "Новый пост №4",
      "author": "admin",
      "group": null,
      "image": null,
      "pub_date": "2022-01-05T08:45:19.129408Z",
      "comments": []
    }
  ]
}
```
__POST-запрос__ на создание новой публикации:

> Поле __text__ является обязательным

`http://127.0.0.1:8000/api/v1/posts/`

```
Зарос:
{
    "text": "Новый пост №4"
}
```

```
Ответ:
{
  "id": 4,
  "text": "Новый пост №4",
  "author": "admin",
  "group": null,
  "image": null,
  "pub_date": "2022-01-05T08:45:19.129408Z",
  "comments": []
}
```

__POST-запрос__ на добавление комментария к публикации:

`http://127.0.0.1:8000/api/v1/posts/{post_id}/comments/`

```
Запрос:
{
    "text": "Тестовый комментарий к посту"
} 
```

```
Ответ:
{
  "id": 1,
  "author": "admin",
  "post": 3,
  "created": "2022-01-05T09:17:45.575284Z",
  "text": "Тестовый комментарий к посту"
}
```

__Получение JWT-токена__

`http://127.0.0.1:8000/api/v1/jwt/create/`

```
Запрос:
{

    "username": "admin2",
    "password": "password123"

}
```

```
Ответ:
{
    "refresh": "string",
    "access": "string"
}
```

### Разработчик проекта

Автор: Maksim Zamyatin  
E-mail: [mm.zamyatin@gmail.com](mailto:mm.zamyatin@gmail.com)
