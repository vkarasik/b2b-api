## Получение прайс-листа

### POST /getPrice/

### Параметры запроса

|Параметр|Тип|Обязательный|Описание|
|---|---|---|---|
| id | array | нет | id товара (соответсвует коду товара из b2b) |

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
HTTP/1.1 202 Accepted
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
| data.products | array | список продуктов |
| data.products.N.id | string | id товара (соответсвует коду товара из b2b) |
| data.products.N.group | string | id категории товара |
| data.products.N.name | string | Наименование товара |
| data.products.N.article | string | SKU товара |
| data.products.N.rest | string | Наличие товара на складе (▀ — мало, ▀▀ — достаточно, ▀▀▀ — много) |
| data.products.N.price | number | Цена товара |
| data.products.N.rrprice | string | Рекомендованная розничная цена |

