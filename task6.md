## Задача 6 - Views
### Дедлайн: понедельник (12:00)

**Ветка:** task6

### т.к. в этой задаче вы не делаете API, роуты должны быть описаны в routes/web.php
### как страница будет выглядеть не критично, это на ваше усмотрение
### для этой домашки вам понадобится API из предыдущих домашек
### желательно сделать какую-нибудь навигацию (через navbar) для удобства проверки и тестирования

### запросы к вашему API нужно делать через JQuery (например при удалении сущности)

### Подзадачи:
1. создать базовый шаблон app (resources/views/layouts/app.blade.php)
2. установить bootstrap 4 (все должно подгружаться в app.blade.php)
3. создать шаблоны каждой страницы которые будут вкложены в базовый шаблон с помощью extends

## Список страниц
1. Работа с группами юзера  (GET: в url передается user_id)
на этой странце должно быть:
- таблица с информацией о группах (при загрузке страницы из controller данные через with передаете в blade)
    1. кнопка удалить которая удаляет группу
- форма добавления группы (после добавления возвращает редиректит на страницу с группами)

2. Работа с профилями
на этой странице должно быть:
- таблица со списком профилей (всех юзеров)
- возможность обновления профиля
- возможность удаления и добавления профиля


## Подсказки (простые, но не самые лучшие способы)
- обновлять страницу сразу после обновления данных в базе
- части страниц вроде блока с таблицей тоже можно выносить во вьюшки - просто возвращать HTML (лучше все таки сделать запрос к API и спарсить)

## Полезные ссылки
1. https://laravel.com/docs/5.8/blade
2. https://getbootstrap.com/
3. https://getbootstrap.com/docs/4.3/getting-started/introduction/
4. navbar: https://getbootstrap.com/docs/4.3/components/navbar/
5. https://laravel.com/docs/5.8/redirects

## Доп задачи: (делать можно как угодно с использованием bootstrap ; если API для этого нет - нужно добавить)
- добавить возможность переименовать каждую сущность (профиль / группа)
- в идеале сделать возможность работы с каждой сущностью (профили группы) без перезагрузки страницы