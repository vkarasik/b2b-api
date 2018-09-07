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
   "order":["97042"]
}
```

### Ответ в случае успеха

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```
```json
{
    "data": [
        {
            "order": "97042",
            "dorder": "2018-09-06 14:57:54",
            "status": "A",
            "sum": "24606.91",
            "products": [
                {
                    "id": false,
                    "name": "Корпус FSP QD-503BGM GAMING ATX Black <USB3.0*1,USB2.0*2,HDA,2*5.25'ext/2*3.5'+2*2.5'int,7*FHFL,12cm reafan,0.5mm,MB=245mm,VGA=350mm,CPUfan=160mm,Window,L=435,W=190,H=465// +PSU QD550 80+>",
                    "qty": "5.00"
                },
                {
                    "id": false,
                    "name": "Корпус FSP QD-503BGM GAMING ATX Black <USB3.0*1,USB2.0*2,HDA,2*5.25'ext/2*3.5'+2*2.5'int,7*FHFL,12cm reafan,0.5mm,MB=245mm,VGA=350mm,CPUfan=160mm,Window,L=435,W=190,H=465// noPSU>",
                    "qty": "1.00"
                }
            ]
        }
    ],
    "code": "ok"
}
```

### Описание полей ответа

|Параметр|Тип|Описание|
|---|---|---|
| data.N.order | string | Номер заказа |
| data.N.dorder | string | Дата заказа |
| data.N.status | string | Статус заказа |
| data.N.sum | string | Сумма заказа |
| data.N.products.N.id | string | id товара |
| data.N.products.N.name | string | Название товара |
| data.N.products.N.qty | string | Количество зарезервированного товара |


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
