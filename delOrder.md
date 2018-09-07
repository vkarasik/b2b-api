## Отмена заказа

### POST /delOrder/

Для авторизации используются ваши текущие логин(**login**):пароль(**password**) в системе b2b.

### Параметры запроса

|Параметр|Тип|Обязательный|Описание|
|---|---|---|---|
| order | array of string | да | список заказов из ответа /addOrder/ |

### Пример запроса

```http
POST /delOrder/
Authorization: Basic
```
```json
{
   "order":["97154"]
}
```

### Ответ в случае успеха

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```
```json
{
    "data": {
        "order": "97154"
    },
    "code": "ok"
}
```

### Описание полей ответа

|Параметр|Тип|Описание|
|---|---|---|
| data.order | string | Номер отмененного заказа |

### Ответ при ошибке авторизации

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```
```json
{"data":"Access denied","code":"error"}
```

### Ответ при запросе с неверным номером заказа

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```
```json
{
    "data": "Order not deleted",
    "code": "error"
}
```