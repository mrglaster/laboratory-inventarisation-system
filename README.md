# Контракт 

## Авторизация

### Регистрация пользователя

Тип запроса: POST 
URL: /inventory/api/users/register
Роль: NONE
Тело запроса: 

```
{
   "first_name": "Ivan",
   "last_name" : "Ivanov",
   "login": "login",
   "password": "password"   
}
```

Ответ: 
```
{
  "status": "ok",
  "token": "token" 
}
```

### Авторизация пользователя 
Тип запроса: POST 
URL: /inventory/api/users/auth/login
Роль: NONE 
Тело: 
{
  "login": "login",
  "password": "password" 
}

## Взятие и сдача инвентаря 

### Взятие инвентаря 

Тип запроса: POST 
URL: /inventory/api/storage/loan
Роль: ROLE_STUDENT
Тело: 

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

Тип запроса: POST 
URL: /inventory/api/storage/return
Роль: ROLE_LABORANT
Тело: 

```
{
  "request_id": "request id",
  "result_quantity: 12,
  "return_ok": true
}
```

### Список взятого пользователем

Тип запроса: POST 
URL: /inventory/api/storage/history/user 
Роль: ROLE_STUDENT 
Тело: 

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


### Список взятого за все время

Тип запроса: POST 
URL: /inventory/api/storage/history/all 
Роль: ROLE_LABORANT
Тело: 

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
      "item_picture": "PICTURE_URL",
      "user": "username" 
    }
  ]
...
}
```


### Добавить существующее оборудование 

Тип запроса: POST 
URL: /inventory/api/storage/add
Роль: ROLE_LABORANT 
Тело:  

```
{
   "item_code": "item_code",
   "item_quantity_added": 12
}
```


### Зарегистрировать новое оборудование 

Тип запроса: POST 
URL: /inventory/api/storage/register 
Роль: ROLE_LABORANT 
Тело: 

```
{
   "item_name": "item_name",
   "cover_b64": "cover in base64 format
}
```


### Получить список существующих вещей 

Тип запроса: GET 
URL: /inventory/api/storage/names/list 
Роль: ROLE_STUDENT 
Ответ: 

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

Тип запроса: GET 
URL: /inventory/api/storage/debtors 
Роль: ROLE_LABORANT
Ответ: 

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

Тип запроса: GET 
URL: /inverntory/api/storage/outofstock
Роль: ROLE_LABORANT 
Ответ: 

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
Тип запроса: GET 
URL: /inventory/api/storage/history 
Роль: ROLE_LABORANT 

Тело: 

```
{
   "item_id": "item_id",
   "order_by": "lend_quantity" // Доступны варианты lend_date, return_date, lend_quantity, none
}
```


Ответ: 

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
