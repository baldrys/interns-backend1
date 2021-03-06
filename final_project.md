## Итоговый проект
### Делать этот проект нужно в новом репозитории, все должно быть в итоге доступно в ветке master

### Типы пользователей
1. Admin
2. Store user
3. Customer

## Список таблиц

1. users - full_name (string), api_token (string), role (enum - Customer(default), Store user, Admin)

2. jobs (создается автоматически)

3. items - store_id (store user's id), name(string)

4. item_ingredient - store_id (store user's id), name(string), price(в USD - float, 2 знака после запятой)

5. item_ingredients - item_id, ingredient_id, amount

6. cart_items - user_id, item_id, amount

7. orders - store_id(user id), customer_id(user id), status (enum) = [Canceled, Placed (default), Approved, Shipped, Received], total_amount

8. stores - name (string)

9. store_users (сотрудники магазина) - store_id, user_id

### Итоговый список роутов (делаем только API)

1. GET      /api/v1/auth/register

регистрация через API
**Пример ответа:**
```
    {
      "success": true,
      "data": {
        "token": "d12hjHduh12dh21"
      }
    }
```

2. GET      /api/v1/auth/login

вход через API
**Пример ответа:**
```
    {
      "success": true,
      "data": {
        "token": "d12hjHduh12dh21"
      }
    }
```

## Customer роуты (доступно только для customer & admin)

3. POST     /api/v1/cart/items

добавляет item в корзину
Параметры: amount

4. DELETE   /api/v1/cart/item/{item}

удаляет item из корзины

**Пример ответа:**
```
    {
      "success": true
    }
```

5. POST     /api/v1/cart/checkout

создает order и считает итоговую сумму из ингридиентов каждого item

6. GET      /api/v1/me/info

получаем инфо о текущем юзере

**Пример ответа:**
```
    {
      "success": true,
      "data": {
        "user": {
          "id": 23,
          "email": "someemail@gmail.com",
          "created_at": "2019-03-12 07:15:40" // можно выводить даты в другом формате
        }
      }
    }
```

7. GET      /api/v1/me/orders

доп параметры:
1. page (по 10 на страницу)

параметры для фильтрации:
1. status прим. "Canceled"
2. min_total_amount 120.50
3. max_total_amount 17.60

получаем все заказы со всеми статусами

**Пример ответа:**
```
    {
      "success": true,
      "data": {
        "orders": [
          {
            "id": 12,
            "user_id": 32,
            "store_id": 2,
            "total_amount": 120.00,
            "items": [
              {
                "item_id": 3,
                "amount": 13
              },
              {
                "item_id": 2,
                "amount": 10
              }
            ]
          }
        ]
      }
    }
```

## Store user роуты (доступно только для customer & admin)

8. POST     /api/v1/store/{store}/items

добавляет item 
параметры: name + массив ingredients

**Пример ответа:**
```
    {
      "success": true,
      "data": {
        "item": {
          "id": 23,
          "store_id": 23,
          "name": "some name",
          "ingredients": []
        },
      }
    }
```

9. PATCH    /api/v1/store/{store}/items

обновляет item 
не обязательные параметры: name + массив ingredients (если массив передан вы затираете текущие ингредиенты новыми)

**Пример ответа:**
```
    {
      "success": true,
      "data": {
        "item": {
          "id": 23,
          "store_id": 23,
          "name": "some name",
          "ingredients": []
        },
      }
    }
```

10. DELETE     /api/v1/store/{store}/items/{item}
**item можно удалить только если он нигде не используется например в оформленных заказах**

**Пример ответа:**
```
    {
      "success": true,
      "data": {
        "deleted_item": {
          "id": 23,
          "store_id": 23,
          "name": "some name",
          "ingredients": []
        },
      }
    }
```

11. GET      /api/v1/store/{store}/orders

доп параметры:
1. page (по 10 на страницу)

параметры для фильтрации:
1. status прим. "Canceled"
2. min_total_amount 120.50
3. max_total_amount 17.60

получаем все заказы магазина

**Пример ответа:**
```
    {
      "success": true,
      "data": {
        "orders": [
          {
            "id": 12,
            "user_id": 32,
            "store_id": 2,
            "total_amount": 120.00,
            "items": [
              {
                "item_id": 3,
                "amount": 13
              },
              {
                "item_id": 2,
                "amount": 10
              }
            ]
          }
        ]
      }
    }
```

## Общий роут для customer и store user (доступно только для customer & admin)

12. PATCH     /api/v1/store/{store}/order/{order}

обновление статуса заказа

параметры:
1. status прим. "Canceled"

Как работает
1. store user может проставить статусы
любой => Canceled
Placed => Approved
Approved => Shipped

2. customer проставить статусы
Shipped => Received
любой кроме Shipped => Canceled

## Роуты администратора

13. POST    /api/v1/store/{store}/users
добавляем store user'а

13. DELETE    /api/v1/store/{store}/users/{user}
удаляем store user'а

## Доп функционал (в идеале реализовать весь)
1. Вход & регистрация через GitHub (можно это сделать в т.ч. во вьюшках - главное по email создать \ обновить инфо юзера и получить токен)
2. Покрытие тестами
3. Использовать transformers
4. для enum'ов в базе использовать myclabs/php-enum или bensampo/laravel-enum при работе со значениями
5. carbon для работы с датами (елси потребуется)
6. swagger по желанию (писать документацию в процессе пока делаете а не после)

## Подсказки
1. total_price item'а можно считать в ItemUtils например и так же сразу это использовать при выводе в трансформере

## Полезные ссылки
1. https://laravel.com/docs/5.8/socialite (этот пакет можно использовать для авторизации через GITHUB)
