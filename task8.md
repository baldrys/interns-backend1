## Задача 8 - swagger и unit тесты
### Дедлайн: вторник (18:00)

**Ветка:** task8

### Подзадачи:
1.  Установите phpunit
2.  попробуйте запустить тесты в своем текущем laravel проекте - все должно работать без ошибок

## Тесты

как тестировать это на ваше усмотрение

вариантов несколько

1й стандартный (перед каждым тестом чистит базу и накатывает все миграции)

работает очень медленно - использует для тестов отдельную бд

по этому способу инструкции ищите сами =)

2й миграции накатываются 1 раз перед стартом всех тестов (отдельная бд то же используется)
1. Добавьте вызов команды migrate
https://github.com/2UP/interns-portal-api/blob/d116472b3054eddffef0bcb91ccbdc3ba87b805b/tests/CreatesApplication.php#L20
2. создайте .env.testing (этот конфиг будет спользоваться для ) - там впишите параметры для доступа к тестовой бд
3. **пример как писать тесты**

в большинстве случаев вам понадобятся данные в базе - например если вы тестируете роут для получения юзера по id (в UserController)
1) создаете tests/Feature/Http/Controllers/UserControllerTests.php (для того что бы phpunit искал тесты в таких файлах добавьте suffix как тут https://github.com/2UP/interns-portal-api/blob/d116472b3054eddffef0bcb91ccbdc3ba87b805b/phpunit.xml#L13)
2) если ваш роут может вернуть 200 с юзером или 404 если юзер не найдет т.е. вам понадобится 2 теста
1. function GetUser_WithUser_Success
2. function GetUser_WithoutUser_NotFound
3) в каждом тесте если вам нужны данные - создаете, тестируете потом данные удаляете

## Swagger

Пример swagger файла: https://github.com/2UP/interns-portal-api/blob/master/swagger-api.json (можно писать в json, можно в YAML)

Добавьте себе в репозиторий такие же ссылки:
+ [Swagger API Docs - VIEW](https://generator.swagger.io/?url=https://raw.githubusercontent.com/2UP/interns-portal-api/master/swagger-api.json)
+ [Swagger API Docs - EDIT](https://editor.swagger.io/?url=https://raw.githubusercontent.com/2UP/interns-portal-api/master/swagger-api.json)

**Нужно оформить документацию для роутов из 3й и 4й домашки**

## Полезные ссылки
1. https://laravel.com/docs/5.8/testing
2. https://dzone.com/articles/7-popular-unit-test-naming (нейминг функций тестов - я использую 1й вариант, вам тоже советую но можете использовать любой из этих)
