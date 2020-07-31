# SendText

Метод предназначен для отправки текстового сообщения корреспонденту или в группу. Если корреспондента нет в контактах аккаунта, то он будет автоматически добавлен в контакты при первой отправке сообщения. Также корреспондента можно добавить в контакты методом [AddContact](../contacts/add-contact.md#cus). 


## Запрос {#request}

Для отправки текстового сообщения требуется выполнить запрос по адресу:
```
POST https://api.green-api.com/v2/{{account}}/SendText
```

### Параметры запроса {#request-parameters}

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`to` | **string** | Да | [Идентификатор корреспондента или группы](../chat-id.md) - получатель сообщения
`text ` | **string** | Да | Текст сообщения. Поддерживаются символы emoji 😃 

> Максимальная длина текстового сообщения составляет 4096 символов

### Пример тела запроса {#request-example-body}

Отправка сообщения корреспонденту:
```json
{
    "to": "79001234567",
    "text": "I use Green-API to send this message to you!"
}
```

Отправка сообщения в группу:
```json
{
    "to": "79001234567-1581234048",
    "text": "I use Green-API to send this message to the Group!"
}
```
## Ответ {#response}

### Поля ответа {#response-parameters}

Поле | Тип |  Описание
----- | ----- | -----
`messageId ` | **integer** | Идентификатор отправленного сообщения 

### Пример тела ответа {#response-example-body}

```json
{
    "messageId": 1234
}
```

### Ошибки SendText {#errors}

Перечень общих для всех методов ошибок смотрите в разделе [Стандартные ошибки](../common-errors.md)

В случае ошибки возвращается код HTTP `400` с подробным описанием ошибки в теле ответа.

### Пример тела ответа с ошибкой {#response-example-body-error}

```json
{
    "errorCode": 82,
    "error": "Превышено колличество исходящих сообщений"
}
```

## Пример кода на Python  {#request-example-python}

```python
import requests

url = "https://api.green-api.com/v2/{{account}}/SendText"

payload = "{\r\n    \"to\": \"79001234567\",\r\n    \"text\": \"I use Green-API to send this message to you!\"\r\n}"
headers = {
  'Authorization': 'Bearer {{apiToken}}',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```