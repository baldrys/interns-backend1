## Задача 2
### Дедлайн: понедельник (12:00)

**Ветка:** task2

**т.к. мы начинаем делать API - ваши роуты должны быть в routes/api.php**

Подзадачи:
1.  Создать миграцию таблицы **user_profiles** со следующей структурой:
    1. id - increments
    2. name - string
    3. user_id - foreign key (id в таблице users) on delete set null
2. Создать модель UserProfile в App/Models/User
3. Создать сидер и заполнять таблицы через php artisan:seed - 10 профилей  с верными данными (например пользователь с данным user_id тоже должен быть добавлен)
4. сделать роуты ниже

**Результат:**
1.  роут GET api/v0/users/profile/{id}

**Пример ответа**
```
    {
      "success": true,
      "data": {
        "profile": {
            "id": 1,
            "name": "Profile 1",
            "user_id": 12
        }
      }
    }
```

2.  роут GET api/v0/user/{userId}/profiles

возвращает все профили пользователя

**Пример ответа**
```
    {
      "success": true,
      "data": {
        "profiles": [
            {
                "id": 1,
                "name": "Profile 1",
                "user_id": 4
            },
            {
                "id": 2,
                "name": "Profile 2",
                "user_id": 4
            },
            ...
        ]
      }
    }
```

3.  роут GET api/v0/users/profiles

возвращает все профили по 5 на страницу, если профилей нет - пустой массив

**Параметры:**
    1. page обязательно >= 1

**Пример ответа**
```
    {
      "success": true,
      "data": {
        "profiles": [
            {
                "id": 1,
                "name": "Profile 1",
                "user_id": 12
            },
            {
                "id": 2,
                "name": "Profile 2",
                "user_id": 4
            },
            ...
        ]
      }
    }
```

4.  роут PATCH api/v0/users/profile/{id}
**Параметры:**
    1. name
обновляет имя профиля

**Пример ответа**
```
    {
      "success": true,
      "data": {
        "profile": {
            "id": 1,
            "name": "Profile 1",
            "user_id": 12
        }
      }
    }
```

5.  роут DELETE api/v0/users/profile/{id}

удаляет профиль

**Пример ответа**
```
    {
      "success": true,
    }
```

## перед продолжением почитайте про SQL injections
**!данные возвращаются в том же формате что и в роутах 1-5, только без ORM а с использованием DB класса**
https://laravel.com/docs/5.7/queries

6.  роут GET api/v0/db/users/profile/{id}

7.  роут GET api/v0/db/user/{userId}/profiles

8.  роут GET api/v0/db/users/profiles

9.  роут PATCH api/v0/db/users/profile/{id}

10.  роут DELETE api/v0/db/users/profile/{id}


## Требования к ендпоинтам

1. Делайте проверки на наличие искомой записи в базе и возвращайте ошибку в случае
```
    abort(404, "%ваша сущность% не найдена")
```

## Что посмотреть \ почитать
1.  Контроллеры
2.  ORM
3.  Migrations
4.  Seeds

## Полезные ссылки
1.  https://laravel.com/docs/5.7/migrations
2.  https://laravel.com/docs/5.7/seeding
3.  https://laravel.com/docs/5.7/eloquent
