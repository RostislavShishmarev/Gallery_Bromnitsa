<table bordercolor="none">
  <tr>
    <td>
      <img src="https://thumb.cloud.mail.ru/weblink/thumb/xw1/5NLU/5toyBN9yG" alt="Логотип" width="55" height="55" />
    </td>
    <td>
      <h1>Фотогалерея "Бромница" — приложение для ПК.</h1>
    </td>
  </tr>
</table>

## _Проект для Яндекс Лицея по модулю PyQt5_

![Главное окно](https://thumb.cloud.mail.ru/weblink/thumb/xw1/XZ9N/tYSjwQzfb)

### Суть
Бромница — аналог мобильного приложения "Галерея" для компьютера. Оно даёт возможность группировать изображения по альбомам, просматривать их и редактировать.

Окна:
- Авторизация — в нём пользователь вводит логин и пароль (приложение рассчитано на нескольких пользователей, но им можно пользоваться и в одиночку)
- Главное — создание альбомов и переход к общим настройкам.
Перейти к альбому можно через нажатие на его обложку.
- Настройки — переключение по видам настроек с помощью верхнего меню, здесь доступны смена темы (4 на выбор), количества колонок сетки альбомов, имени и фото пользователя, логина и пароля, а также места, где хранится ваша база данных.
- Альбом — сетка картинок с названиями, переход к настройкам конкретного альбома.
Нажатие на картинку — просмотр изображения.
- Настройки альбома — смена названия, обложки и количества колонок сетки картинок альбома.
- Изображение — просмотр, переименование, удаление и переход к редактору.
- ИЗОбработчик (он же редактор) — первичная обработка картинки: несколько фильтров и регулирование компонентов.

![ИЗОбработчик](https://thumb.cloud.mail.ru/weblink/thumb/xw1/HDuL/giuUu2jKN)

### Сборка
##### Вариант №1 (для пользователей):
1. Загрузить файл Bromnitsa.exe из последнего релиза
2. Скопировать его в папку, где будет храниться приложение
3. Запустить его

Примечание: приложение создаёт в папке, где оно находится, папку db, в которой хранятся все ваши данные. Если вы не хотите их потерять, её нужно перемещать вместе с exe-файлом.
##### Вариант №2 (для разработчиков):
1. Загрузить последний релиз и файл Additional.zip
2. Перенести содержимое релиза в свободную папку
3. Перенести папки images и ui из Additional.zip в корень проекта (туда, где находится main.py)
4. Установить зависимости:
```sh
pip install -r requirements.txt
```
5. Запустить файл main.py

Примечание: в папке ui находятся ui-файлы, использованные для создания приложения. Для работы программы их наличие необязательно.

### Код

В проекте использован язык python. Пользовательский интерфейс создан с помощью библиотеки [PyQt5](https://pypi.org/project/PyQt5/). Также были использованы [Pillow](https://pypi.org/project/Pillow/), [numpy](https://pypi.org/project/numpy/) и [opencv-python](https://pypi.org/project/opencv-python/) (для редактора изображений).

Структура проекта:
- main.py — основной код, главное окно и настройки.
- album_module.py — альбом и его настройки.
- image_module.py — просмотр изображений, ИЗОбработчик и всё, что с ним связано.
- helpers.py — вспомогательные функции и классы.
- ui_module.py — классы интерфейса.
- images (директория) — изображения для работы программы.

Особый интерес может представить функция to_pixmap из файла helpers.py — конвертер Pillow-изображения в QtGui.QPixmap:
```python
from PyQt5 import QtGui


def to_pixmap(foto):
    '''Конвертирует PIL изображение в QPixmap'''
    foto = foto.convert("RGBA")
    qim = QtGui.QImage(foto.tobytes("raw", "RGBA"), foto.size[0],
                       foto.size[1], QtGui.QImage.Format_RGBA8888)
    return QtGui.QPixmap.fromImage(qim)

```
