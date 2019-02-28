## Задача 4
### Дедлайн: четверг (12:00)

**Ветка:** task4

Подзадачи:
1.  Добавить пару колонок в таблицу users
    1.    api_token    string
    2.    banned       boolean - default false
    3.    role         ['User', 'Admin'] - default = 'User'

    https://stackoverflow.com/questions/28547038/add-default-value-to-enum-type-field-in-schema-builder
    
2.  Добавить новые роуты (api/v1) в группу с middleware auth:api
3.  Добавить кастомный middleware StopBanned

3.1 Делать проверку флага у юзера (в лк есть пример) если banned = true возвращаем abort 403 с сообщением "Your account was banned"
4.  Добавить кастомный middleware AdminOnly

4.1 Делать проверку enum'а role у юзера должен быть = Admin

## Пример
https://github.com/2UP/interns-portal-api/blob/master/routes/api_v1.php

# Список роутов (результат)

1. GET     api/v1/auth/login

### Параметры
1. email     - string
2. password  - string

## Требования
1. нужно вернуть api_token из таблицы users
2. если комбинация email & пароля неправильная, вернуть: 401 - Unauthorized

**Пример ответа:**
```
    {
      "success": true,
      "data": {
        "token": "d12hjHduh12dh21"
      }
    }
```

2. GET     api/v1/auth/logout
    1. нужно найти юзера по токену (если не найден вернуть 404)
    2. затем обновить этот токен через str_random и вернуть true
    
**Параметры:**
1. api_token

**Пример ответа:**
```
    {
      "success": true,
    }
```

3. GET     api/v1/users

**Параметры:**
1. api_token
2. page - default = 1 - по 5 на страницу

**Middleware:**
api:auth + admin_only + stop_banned

**Пример ответа: (выводить через resource - а лучше через transformer)**
```
    {
      "success": true,
      "data": {
          "users": [
            {
                "id": 1,
                "name": "Ivanov Ivan"
                "email": "someemail1@bk.ru",
                "role": "User",
                "banned": true
            },
            {
                "id": 2,
                "name": "Ivanov Ivan"
                "email": "someemail2@bk.ru",
                "role": "Admin",
                "banned": false
            },
          ]
      }
    }
```

4. PATCH     api/v1/user/{userId}

Обновляем инфу юзера

**Middleware:**
api:auth + admin_only + stop_banned

**Параметры:**
1. name
2. role
3. banned - boolean

**Пример ответа: (выводить через resource - а лучше через transformer)**
```
    {
        "success": true,
        "data": {
            "user": {
                "id": 1,
                "name": "My name"
                "email": "someemail1@bk.ru",
                "role": "User",
                "banned": false
            },
        }
    }
```

## Для того что бы работать с enum в laravel можно использовать laravel-enum
https://github.com/BenSampo/laravel-enum

## Доп инфо
1. api_token создается с помощью str_random(30)

## Полезные ссылки
1.  https://medium.com/@danielalvidrez/how-to-use-laravels-built-in-token-auth-6b6f6c26d059
2.  https://stackoverflow.com/questions/46425133/laravel-5-5-api-authorization-with-api-token
3.  https://laravel.com/docs/5.7/authorization
4.  https://laravel.com/docs/5.7/middleware

## Доп задание
Выводить данные через трансформеры (используя пакет laravel-fractal)

### Пример: (не обязательно делать так же)
https://github.com/2UP/interns-portal-api/blob/master/app/Http/Transformers/V1/User/UserTransformer.php

## дополнительно: если сможете разобраться - сразу выносите валидацию в Request
https://laravel.com/docs/5.7/validation#form-request-validation
