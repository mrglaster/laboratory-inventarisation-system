# Контракт 

## Авторизация

### Регистрация пользователя

Тип запроса: POST <br>
URL: /inventory/api/users/register <br>
Роль: NONE <br>
Тело запроса: <br>

```
{
   "first_name": "Ivan",
   "last_name" : "Ivanov",
   "login": "login",
   "password": "password"   
}
```

Ответ: <br>
```
{
  "status": "ok",
  "token": "token" 
}
```

### Авторизация пользователя 
Тип запроса: POST <br>
URL: /inventory/api/users/auth/login <br>
Роль: NONE <br>
Тело: <br>

```
{
  "login": "login",
  "password": "password" 
}
```

## Взятие и сдача инвентаря 

### Взятие инвентаря 

Тип запроса: POST <br>
URL: /inventory/api/storage/loan <br>
Роль: ROLE_STUDENT <br>
Тело:  <br>

```
{
  "item_code": "code",
  "item_quantity": 12,
  "destination": "room 403"  
}
```

Ответ: 

```
{
  "status": "ok" 
}
```

### Сдача инвентаря 

Тип запроса: POST <br> 
URL: /inventory/api/storage/return <br>
Роль: ROLE_LABORANT <br>
Тело:  <br>

```
{
  "request_id": "request id",
  "result_quantity: 12,
  "return_ok": true
}
```

### Получить информацию о запросе 

Тип запроса: POST <br> 
URL: /inventory/api/storage/request/info <br>
Роль: ROLE_LABORANT <br>
Тело:  <br>

```
{
  "request_id": "request_id" 
}
```

Ответ: 

```
{
   "user_name": "user_name",
   "item_name": "item_name",
   "item_quantity": 12,
   "destination": "room 412"
}
```


### Список взятого данным пользователем

Тип запроса: POST <br>
URL: /inventory/api/storage/history/user <br>
Роль: ROLE_STUDENT <br>
Тело: <br>

```
Тело отсутствует, используем данные из bearer token
```

Ответ: 

```
{
  "items": [
    {
      "request_id": "request_id",
      "item_name": "item name",
      "item_quantity": 28,
      "returned": true,
      "loan_date": "DATETIME",
      "return_date": "DATETIME",
      "item_picture": "PICTURE_URL"
    }
  ]
...
}
```


### Список взятого конкретным пользователем

Тип запроса: POST <br>
URL: /inventory/api/storage/history/user/specific <br>
Роль: ROLE_LABORANT <br>
Тело: <br>

```
{
    "user_id": "user_id
}
```

Ответ: <br>

```
{
  "items": [
    {
      "request_id": "request_id",
      "item_name": "item name",
      "item_quantity": 28,
      "returned": true,
      "loan_date": "DATETIME",
      "return_date": "DATETIME",
      "item_picture": "PICTURE_URL"
    }
  ]
...
}
```


### Список взятого за все время

Тип запроса: POST <br>
URL: /inventory/api/storage/history/all <br>
Роль: ROLE_LABORANT <br>
Тело: <br>

```
Тело отсутствует, используем данные из bearer token
```

Ответ: <br>

```
{
  "items": [
    {
      "request_id": "request_id",
      "item_name": "item name",
      "item_quantity": 28,
      "returned": true,
      "loan_date": "DATETIME",
      "return_date": "DATETIME",
      "item_picture": "PICTURE_URL",
      "user": "username" 
    }
  ]
...
}
```


### Добавить существующее оборудование 

Тип запроса: POST <br>
URL: /inventory/api/storage/add <br>
Роль: ROLE_LABORANT  <br>
Тело:  <br>

```
{
   "item_code": "item_code",
   "item_quantity_added": 12
}
```


### Зарегистрировать новое оборудование 

Тип запроса: POST <br>
URL: /inventory/api/storage/register <br>
Роль: ROLE_LABORANT <br>
Тело: <br>

```
{
   "item_name": "item_name",
   "cover_b64": "cover in base64 format
}
```


### Получить список существующих вещей 

Тип запроса: GET <br>
URL: /inventory/api/storage/names/list <br>
Роль: ROLE_STUDENT <br>
Ответ: <br>

```
  {
  "items": [
    {
      "item_name": "pink unicorn",
      "item_quantity": 228,
      "item_picture": "picture_url"
    }
  ]
}

```

### Получить список должников 

Тип запроса: GET <br> 
URL: /inventory/api/storage/debtors <br>
Роль: ROLE_LABORANT <br>
Ответ: <br>

```
{
  "debtors": [
    {
      "user_id": "user_id",
      "requests": [
        "request_id1",
        "request_id2"
      ]
    }
  ]
}
```

### Получить список закончившегося оборудования 

Тип запроса: GET <br>
URL: /inverntory/api/storage/outofstock <br>
Роль: ROLE_LABORANT <br>
Ответ: <br>

```
{
  "items": [
    {
      "item_id": "item_id",
      "item_name": "item_name",
      "item_picture": "PICTURE_URL"
    }
  ]
}
```

### Получить историю взятия конкретного оборудования 
Тип запроса: GET <br>
URL: /inventory/api/storage/history <br>
Роль: ROLE_LABORANT <br>
<br>
Тело: <br>

```
{
   "item_id": "item_id",
   "order_by": "lend_quantity" // Доступны варианты lend_date, return_date, lend_quantity, none
}
```


Ответ: <br>

```
{
  "history": [
    {
      "request_id": "request_id",
      "lend_date": "DATETIME",
      "return_date": "DATETIME",
      "lend_quantity": 12
    }
  ]
}
```
