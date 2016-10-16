LOLBOT
========

Асинхронный чат-бот для ВКонтакте.
Идеально подходит как помощник в конференциях.

**ВНИМАНИЕ**
Для работы бота необходим Python версии 3.5 и выше, с версиями ниже бот **не работает** и поддержка старых версий не планируется.
Работоспособность проверена **исключительно на ОС семейства Linux**.

## Начальная настройка
1. Зайдите в папку с ботом (через консоль) и выполните команду `pip3 install -r requirements.txt`. Это автоматически установит все нужные модули.
2. Запустите бота, чтобы он создал файл `settings.py` - `python3 lolbot.py`.
3. **В `settings.py` замените `token` на access_token группы или `vk_login` и `vk_password` на логин и пароль аккаунта ВК соответственно.** 
4. Запустите `python3 lolbot.py` (если вам нужно запустить бота в фоне, используйте `screen` под Linux).

## Смена префиксов
По умолчанию бот отзывается на шесть префиксов: `lolbot`, `лолбот`, `лб`, `файнбот`, `фб`,`!`. 
Сменить их можно в `settings.py` на 10 строке.

## Плагины
* Приветствие (Плагин приветствия)
* Список плагинов (Список загруженных плагинов)
* Музыка (Список музыки из ваших рекомендаций в ВК)
* Случайное число (Случайное число в диапазоне от 1 до 6)
* Случайные мемы (Берутся из паблика, указанного в плагине memes.py)
* Случайные картинки с Двача (Берутся из паблика, указанного в плагине 2ch.py)
* Ближайшие дни рождения в группе (Берутся из паблика, указанного в плагине hday.py)
* Курс валют (Отображение основных курсов валют)
* Список команд (Список всех команд бота `! команды`)
* Шар восьмерка (Решает за вас)
* Время (Показывает текущую дату и время)
* Статистика бота (Показывает данные о счетчиках аккаунта)
* Онлайн серверов FineMine (По фану, чтобы на сайт не заходить)
* Случайные картинки из группы FineMine (Берутся из паблика, указанного в fmgroup.py)
* Отправка смайла (Отправляется "Луна", moon.py)
* Отправка видео (Отправляется "Nope.avi", nope.py)

## Примечание
Для того, чтобы узнать ID пользователя или паблика, используйте https://vk.com/linkapp

## Создание плагинов
В папке plugins есть пример плагина в файле example.py, отвечающий на команду `лб примерплагина`
Там есть и другие плагины, код которых можно просмотреть для понимания того, что можно сделать с помощью бота.

Каждый плагин должен иметь экземпляр класса Plugin (из plugin_system) под именем(обязательно) plugin, вот пример простого плагина:
```python
# импортируем класс Plugin
from plugin_system import Plugin
# создаём объект класса, через него мы будем "подписываться" на команды
plugin = Plugin('Имя плагина')

# использование async и await обязательно, т.к. бот асинхронный
@plugin.on_command('ты тута?')
async def test(vk, msg, args):
    await vk.respond(msg, {'message':'Я тутачки!'})
```

Плагины размещаются в папке `plugins`. Если два плагина имеют одинаковые команды - они обрабатываются в обоих плагинах.
Плагины могут работать со всеми методами API ВКонтакте.