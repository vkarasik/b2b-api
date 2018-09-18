## Получение прайс-листа

### POST /getPrice/

Для авторизации используются ваши текущие логин(**login**):пароль(**password**) в системе b2b.

### Параметры запроса

|Параметр|Тип|Обязательный|Описание|
|---|---|---|---|
| id | array of strings | нет | id товара (соответсвует коду товара в b2b) |

Запрос без параметров возвращает полный актуальный прайс-лист.

### Пример запроса

```http
POST /getPrice/
Authorization: Basic
```
```json
{
    "id": ["SP00005504"]
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
        "groups": [
            {
                "id": "1182",
                "name": "Печатная техника",
                "groups": [
                    {
                        "id": "1185",
                        "name": "Расходные материалы",
                        "groups": [
                            {
                                "id": "2411",
                                "name": "Струйные картриджи"
                            }
                        ]
                    }
                ]
            }
        ],
        "products": [
            {
                "id": "SP00005504",
                "group": "2411",
                "name": "Картридж CL-446XL &lt;MG2440, MG2540&gt;",
                "article": "8284B001AA",
                "rest": "▀",
                "price": 46.7,
                "rrprice": ""
            }
        ]
    },
    "code": "ok"
}
```

### Описание полей ответа

|Параметр|Тип|Описание|
|---|---|---|
| data.groups | array | список групп/подгрупп для запрошенных id |
| data.products | array | список товаров |
| data.products.N.id | string | id товара (соответсвует коду товара в b2b) |
| data.products.N.group | string | id группы товара |
| data.products.N.name | string | Наименование товара |
| data.products.N.article | string | SKU (артикул) товара |
| data.products.N.rest | string | Наличие товара на складе ("▀" — мало, "▀▀" — достаточно, "▀▀▀" — много, "0" — товар не найден) |
| data.products.N.price | number | Цена BYN с НДС |
| data.products.N.rrprice | string | Рекомендованная розничная цена BYN с НДС |

### Ответ при ошибке авторизации

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```
```json
{"data":"Access denied","code":"error"}
```

### Ответ при запросе единственного неверного id

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```
```json
{
    "data": "Products not found",
    "code": "error"
}
```

В случае если неверный **id** запрошен в массиве с верными, ответ будет как в случае успеха, но для неверного **id** вернется **"rest" :  "0"**

### Пример запроса c неверным/несуществующим id

```http
POST /getPrice/
Authorization: Basic
```
```json
{
    "id": ["SP00005504","SP00000000"]
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
        "groups": [
            {
                "id": "1182",
                "name": "Печатная техника",
                "groups": [
                    {
                        "id": "1185",
                        "name": "Расходные материалы",
                        "groups": [
                            {
                                "id": "2411",
                                "name": "Струйные картриджи"
                            }
                        ]
                    }
                ]
            }
        ],
        "products": [
            {
                "id": "SP00005504",
                "group": "2411",
                "name": "Картридж CL-446XL &lt;MG2440, MG2540&gt;",
                "article": "8284B001AA",
                "rest": "▀",
                "price": 46.7,
                "rrprice": ""
            },
            {
                "id": "SP0000000",
                "rest": "0"
            }
        ]
    },
    "code": "ok"
}
```
