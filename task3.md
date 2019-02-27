## Задача 3
### Дедлайн: четверг (12:00)

**Ветка:** task3

Подзадачи:
1.  Создать миграцию и модель UserGroup (таблица user_group)
    Список полей:
    1. id
    2. name - string

    Так же сделать:
    + сидер (10-15 записей)

2.  Создать миграцию и модель UserGroups (таблица user_groups)
    Список полей:
    1. id
    2. user_id  - foreign key on delete cascade 
    (при удалении записи из users эта запись должна удалиться вместе с ней)
    2. group_id - foreign key on delete cascade 
    (при удалении записи из user_group эта запись должна удалиться вместе с ней)
    

    https://stackoverflow.com/questions/43094543/what-does-ondeletecascade-mean

    Так же сделать:
    + сидер (20-25 записей)

# Список роутов (результат)

1. POST     api/v0/users/group

добавляем группу

### Параметры
name - string

**Пример ответа:**
```
    {
      "success": true,
      "data": {
        "created_group": {
            "id": 1,
            "name": "Group 1"
        }
      }
    }
```

2. GET      api/v0/user/{userId}/groups

получаем группы пользователя

**Пример ответа:**
```
    {
      "success": true,
      "data": {
        "groups": [
            {
                "id": 1,
                "name": "Group 1"
            },
            {
                "id": 12,
                "name": "Group 3"
            },
            ...
        ]
      }
    }
```

3. DELETE api/v0/users/groups/{groupId}

удаляет группу

**Пример ответа:**
```
    {
      "success": true,
    }
```

4. POST api/v0/user/{userId}/group/{groupId}


добавляет пользователя к группе

**Пример ответа:**
```
    {
      "success": true,
    }
```

5. DELETE api/v0/user/{userId}/group/{groupId}

убирает пользователя из группы

**Пример ответа:**
```
    {
      "success": true,
    }
```

# Требования к роутам
1. Выводить результат нужно с помощью Laravel resourse
2. нужно делать валидацию входных параметров - пример:
Раздел 'Writing The Validation Logic' https://laravel.com/docs/5.7/validation

3. Разобраться с Relations - https://laravel.com/docs/5.7/eloquent-relationships
и использовать one to many / many to many

# дополнительно: если сможете разобраться - сразу выносите валидацию в Request
https://laravel.com/docs/5.7/validation#form-request-validation


! У пользователя может быть несколько групп одновременно

## Полезные ссылки
1.  https://medium.com/@dinotedesco/laravel-api-resources-what-if-you-want-to-manipulate-your-models-before-transformation-8982846ad22c
2.  https://laravel.com/docs/5.7/eloquent-resources

# Вопросы ответы
### Валиадция параметров, там же параметр только 1 в первом запросе(name  - POST api/v0/users/group)  только его валидировать? А для проверки параметров в url (api/v0/user/{userId}/group/{groupId}) как ты говорил, лучше model bindings использовать.
Да
### Правильно ли я понимаю что между users и groups на самом деле отношение многие ко многим и эта связь через дополнительную таблицу user_groups.
Да

