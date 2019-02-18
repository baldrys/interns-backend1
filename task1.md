## Задача 1 
### Дедлайн: четверг в 12:00 (22.02.2019)

**Ветка:** task1

Подзадачи:
1.  Развернуть laravel проект
2.  Залить проект на github в ваш профиль
3.  Разобраться с .env
4.  создать Task1Controller - поместить в app/Http/Controllers/Task1
5.  создать роут GET task1/hello_world - связать с Task1Controller@helloWorld
6.  создать роут GET task1/uuid - связать с Task1Controller@uuid
6.  установить (найти в packagist.org) ramsey/uuid и сделать роут /task1/uuid (пример ниже)
7.  создать роут GET task1/data_from_config
8.  добавьте TEST_CONFIG_VALUE="someData" в .env файл

**Результат:**
1.  роут GET task1/hello_world - возвращает строку "Hello world"
2.  роут GET task1/uuid - возвращает сгенерированный Uuid::uuid1(); в формате:
  
**/task1/uuid должен возвращать данные в следующем формате, через response()->json()**

```
    {
      "success": true,
      "data": {
        "uuid": "сгенерированный uuid1"
      }
    }
```

3.  роут GET task1/data_from_config - возвращает данные из .env файла (TEST_CONFIG_VALUE) 

```
    {
      "success": true,
      "data": {
        "config_data": "Ваше Значение TEST_CONFIG_VALUE Из .env Файла"
       }
    }
```


**Что посмотреть \ почитать**
1.  Контроллеры
2.  Как работает git / composer
3.  Route group
4.  response()->json()

**Полезные ссылки**
1.  https://laravel.ru/docs/v5
2.  https://laravel.ru/docs/v5/configuration
3.  https://laravel.com/docs/5.7/responses#json-responses
