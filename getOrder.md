## Получение состояния заказа

### POST /getOrder/

### Параметры запроса

|Параметр|Тип|Обязательный|Описание|
|---|---|---|---|
| order | array of string | да | список заказов из ответа /addOrder/ |

### Пример запроса

```http
POST /getOrder/
Authorization: Basic
```
```json
{
   "products":[
      {
         "id":"SP00009726",
         "qty":1
      }
   ]
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
        "order": 97007
    },
    "code": "ok"
}
```

### Описание полей ответа

|Параметр|Тип|Описание|
|---|---|---|
| data.order | number | Номер созданного заказа |


### Ответ при ошибке авторизации

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```
```json
{"data":"Access denied","code":"error"}
```

### Ответ при запросе с единственным неверным id

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```
```json
{
    "data": "Products not available",
    "code": "error"
}
```

В случае если товар с неверным **id** отправлен в массиве с верными, ответ будет как в случае успеха, но товар с неверным **id** не попадет в заказ

### Пример запроса c неверным/несуществующим id

```http
POST /getOrder/
Authorization: Basic
```
```json
{
   "products":[
      {
         "id":"SP00009726",
         "qty":1
      },
      {
         "id":"SP00000000",
         "qty":1
      }
   ]
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
        "order": 97011
    },
    "code": "ok"
}
```
