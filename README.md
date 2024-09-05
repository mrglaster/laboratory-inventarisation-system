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
  "consumtion_percent": 12,
  "return_ok": true
}
```


