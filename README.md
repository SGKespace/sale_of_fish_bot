# tg_bot
Учебный проект dvmn

Этот Telegram-бот, вариант онлайн рыбного магазина (можно выбирать товар, добавлять в корзину, просматривать что в корзине, удалять). 
Бот использует [Elastic Path API](https://elasticpath.dev/docs/pxm/products/ep-pxm-products-api/get-a-product) для получения информации о продуктах c [сервиса Moltin](https://www.moltin.com/) который пепреадресует на https://www.elasticpath.com/, созданные данные (корзины и информация о клиентах) помещаются в базу данных  [Redislabs](https://redislabs.com/).

# Внимание
1. База данных   [Redislabs](https://redislabs.com/)   работает только через VPN
2. Elastic Path API находится в процессе коррекции и работает очень не стабильно, на момент написания  много неточностей.
3. Не нужно  даже пробовать использовать другие версии библиотек (напрмер в Редис повышение приведет [к ошибке с авторизацией](https://github.com/redis/node-redis/issues/1591) , в Телеграм возникнут проблемы с update.message и т.д.) - это старинные, но СТАБИЛЬНЫЕ  версии.
4. Все данные о товаре в Moltin заполнять только латинскими буквами, SKU обязатеьно должен содержать буквы, все поля должны быть заполнены (вплоть до комментария  к товару), прайс должен быть создан, фотографию товара можно не загружать, но если решитесь - обратите внимание на размер, если будет большим магазин не напишет ошибки, но API шка вылетит с ошибкой.

## Требования к окружению

Получите токены  [Телеграм](https://t.me/BotFather), затем определите [chat_id](https://t.me/messageinformationsbot)  поместите в переменные окружения (файл .env). REDIS_DB_URL=redis://[[username]:[password]]@host:port/database Вы можете прочитать эту часть [документации Redis](https://redis.readthedocs.io/en/latest/connections.html#redis.Redis), чтобы узнать больше о типах URL-адресов баз данных, к которым может подключаться Redis.

Пример файла:

```
EP_CLIENT_ID='tNgAvzjlsdvferNJNLRLGZA39ml'
EP_CLIENT_SECRET='q9mHGGgUGkkhBNKJkbkdnvfnk6bwd55odanG'
EP_API_URL='https://useast.api.elasticpath.com'
EP_PRICE_BOOK_ID='46ddefdsd7d-9cdsd-44e9-bdfsd-d9d1dsvsvf92'
CART_ID='2f525340-beb1-4cc8-5646t2-342353255212cd4'
TELEGRAM_TOKEN='595436346261:AAHbhBJFjKlbZF8Fosdgvdfge4Jv6Zweeg'
TG_LOG_CHAT_ID=123456789
REDIS_DB_URL=redis://default:sC1mOzyuuwGOvлпПР4FrEAoAQUw8G@redis-18998.c84.us-east-1-2.ec2.cloud.redislabs.com:18998/Sergey-free-db

``` 

Python 3.xx и выше (должен быть уже установлен)

``` 
python-telegram-bot==13.0
requests==2.31.0
environs==9.5.0
redis==3.0.1
``` 

Можно установить командой  
``` 
PIP install -r requirements.txt
```

Запускать бота осууществляется с помощью команды

``` 
python tg_bot.py
```


## Отказ от ответственности

Автор программы не несет никакой ответственности за то, как вы используете этот код или как вы используете сгенерированные с его помощью данные. Эта программа была написана для обучения автора и других целей не несет. Не используйте данные, сгенерированные с помощью этого кода в незаконных целях.
