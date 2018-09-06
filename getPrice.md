## Получение прайс-листа

### POST /getPrice/

### Параметры запроса

|Параметр|Тип|Обязательный|Описание|
|---|---|---|---|
| id | array &#124; array of strings | нет | id товара (соответсвует коду товара из b2b) |

Запрос без параметров — возвращает полный актуальный прайс лист

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
| data.products.N.id | string | id товара (соответсвует коду товара из b2b) |
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
