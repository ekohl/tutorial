# Ваш перший Django проект!

> Part of this chapter is based on tutorials by Geek Girls Carrots (https://github.com/ggcarrots/django-carrots).
> 
> Частини цієї глави засновані на [jango-marcador tutorial](http://django-marcador.keimlink.de/), який є дозволеним міжнародною ліцензією ShareAlike 4.0 від Creative Commons Attributes. Авторське право на навчальні матеріали django-marcador tutorial належить Markus Zapke-Gründemann та ін.

We're going to create a small blog!

Перший крок - це почати новий проект Django. По суті, це означає що ми запустимо деякі скрипти, які надає Django, що створять для нас скелет Django проекту. Це просто кілька каталогів та файлів, якими ми користуватимемось пізніше.

Імена деяких файлів і папок є дуже важливими для Django. Не можна перейменовувати файли, які ми зараз будемо створювати. Їх переміщення в різні місця також не є хорошою ідеєю. Для того щоб Django міг знаходити важливі речі, потрібно підтримувати задану архітектуру.

> Пам'ятайте, що усе треба запускати у віртуальному середовищі. Якщо ви не бачите префікс `(myvenv)` в консолі, то потрібно активувати ваше віртуальне середовище. Ми пояснювали як це зробити у розділі **Встановлення Django** в частині **Робота з віртуальним середовищем**. Набираючи `myvenv\Scripts\activate` на Windows чи `source myvenv/bin/activate` на Mac OS X або Linux зробить це для Вас.

<!--sec data-title="Create project: OS X or Linux" data-id="django_start_project_OSX_Linux" data-collapse=true ces-->

На Вашій Mac OS X чи Linux консолі, Ви повинні виконати наступну команду.**Не забувайте додати крапку`.`в кінці!**

{% filename %}command-line{% endfilename %}

    (myvenv) ~/djangogirls$ django-admin startproject mysite .
    

> Крапка `.` має вирішальне значення, оскільки вона означає "встанови Django в поточний каталог" (символ крапки `.` використовується щоб не писати повний шлях).
> 
> **Примітка**Набираючи вище зазначену команду, пам'ятайте, що Ви набираєте тільки частину, яка починається з `django-admin`. Частина `(myvenv) ~/djangogirls$`, показана тут, є лише прикладом підказки, яка запропонує ввести дані у Вашому командному рядку.

<!--endsec-->

<!--sec data-title="Create project: Windows" data-id="django_start_project_windows" data-collapse=true ces-->

На Windows Ви повинні виконати наступну команду. **(Не забувайте додавати крапку`. в кінці)</strong>:</p>

<p>{% filename %}command-line{% endfilename %}</p>

<pre><code>(myvenv) C:\Users\Name\djangogirls> django-admin.exe startproject mysite .
`</pre> 

> Крапка `.` має вирішальне значення, оскільки вона означає "встанови Django в поточний каталог" (символ крапки `.` використовується щоб не писати повний шлях).
> 
> **Примітка**Набираючи вище зазначену команду, пам'ятайте, що Ви набираєте тільки частину, яка починається з `django-admin.exe`. Частина `(myvenv) C:\Users\Name\djangogirls>`, показана тут, є лише прикладом підказки, яка запропонує ввести дані у Вашому командному рядку.

<!--endsec-->

`django-admin.py` - це скрипт, що створить для вас усі необхідні папки і файли. Наразі ви повинні мати структуру, котра виглядає наступним чином:

    djangogirls
    ├── manage.py
    ├── mysite
    │   ├── asgi.py
    │   ├── __init__.py
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
    ├── myvenv
    │   └── ...
    └── requirements.txt
    

> **Примітка**: у Вашій структурі каталогів, Ви також побачите Ваш `myvenv` каталог, який ми створили раніше.

`manage.py` - це скрипт, який допомагає з управлінням сайтом. Завдяки йому ми зможемо (серед іншого) запустити вебсервер на Вашому комп'ютері без установки чого-небудь ще.

Файл `settings.py` містить конфігурацію вашого веб сайту.

Пам'ятаєте, коли ми розмовляли про листоношу, що перевіряє, куди треба доправити листа? Файл `urls.py` містить список шаблонів, що використовуються елементом `urlresolver`.

Проігноруємо поки інші файли, адже ми не будемо їх змінювати. Єдина річ, яку варто пам'ятати - не видалити їх ненароком!

## Зміна налаштувань

Здійснимо деякі зміни в `mysite/settings.py`. Відкриємо файл в текстовому редакторі, який ви мали встановити раніше.

**Примітка**: Майте на увазі, що `settings.py` є звичайним файлом, як і будь-який інший. Ви можете відкрити його зсередини кодового редактору, використовуючи меню "file -> open". Це дозволить Вам відкрити звичайне вікно, в якому Ви зможете перейти до Вашого `settings.py` файлу та вибрати його. Крім того, Ви можете відкрити файл, якщо перейдете в папку the djangogirls на Вашому робочому столі, натискаючи на неї правою кнопкою миші. Після цього виберіть Ваш редактор коду зі списку. Вибір редактора є важливим через те, що у вас можуть бути встановлені інші програми, які можуть відкрити файл, але не дозволять вам його редагувати.

Було б непогано мати коректний час на нашому сайті. Перейдіть в [Wikipedia's list of time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) і скопіюйте відповідний часовий пояс (TZ) (e.g. `Europe/Berlin`).

У файлі `settings.py`, знайдіть рядок, що містить `TIME_ZONE` і змініть його, щоб вибрати Ваш часовий пояс. Наприклад:

{% filename %}mysite/settings.py{% endfilename %}

```python
TIME_ZONE = 'Europe/Berlin'
```

Мовний код складається з мови, наприклад: `en` для англійців або `de` для німців, і код країни, наприклад: `de` для Німеччини або `ch` для Швейцарії. Якщо англійська не є Вашою рідною мовою, Ви можете додати це, щоб змінити кнопки за замовчуванням і сповіщення від Django відповідно до Вашої мови. Таким чином, у вас буде кнопка "Скасувати", перекладена на мову, яку ви визначили тут. До [Django додається велика кількість підготовлених перекладів](https://docs.djangoproject.com/en/3.2/ref/settings/#language-code).

Якщо Вам потрібна інша мова, змініть мовний код, змінивши наступний рядок:

{% filename %}mysite/settings.py{% endfilename %}

```python
LANGUAGE_CODE = 'de-ch'
```

Нам також потрібно буде додати шлях для статичних файлів. (Ми дізнаємося все про статичні файли та CSS пізніше в цьому уроці.) Опустіться до *кінця* файлу, і просто під вхід `STATIC_URL`, додайте новий під назвою `STATIC_ROOT`:

{% filename %}mysite/settings.py{% endfilename %}

```python
STATIC_URL = '/static/'
STATIC_ROOT = BASE_DIR / 'static'
```

Коли `DEBUG` є `True` і `ALLOWED_HOSTS` порожній, хост перевіряється на відповідність `['localhost', '127.0.0.1', '[::1]']`. Це не буде відповідати вашому імені хоста в PythonAnywhere, при розгортанні нашого додатку, тому ми змінимо наступні налаштування:

{% filename %}mysite/settings.py{% endfilename %}

```python
ALLOWED_HOSTS = ['127.0.0.1', '.pythonanywhere.com']
```

> **Примітка**: Якщо ви використовуєте Chromebook, додайте цей рядок у нижній частині вашого settings.py файл: `MESSAGE_STORAGE = 'django.contrib.messages.storage.session.SessionStorage'`
> 
> Також додайте`.amazonaws.com` до `ALLOWED_HOSTS`, якщо Ви використовуєте cloud9
> 
> Якщо Ви розміщуєте Ваш проєкт на `Glitch.com`, дозвольте нам захистити секретний ключ the Django, який має залишатися конфіденційним (в іншому випадку, будь-хто, ремікшуючий Ваш проєкт, зможе його побачити):
> 
> - Спочатку ми створимо випадковий секретний ключ. Відкрийте термінал Glitch знову і наберіть наступну команду:
>     
>     {% filename %}command-line{% endfilename %}
>     
>     ```bash
>     python -c 'from django.core.management.utils import get_random_secret_key; \
>           print(get_random_secret_key())'
>     ```
>     
>     Це має зобразити довгу випадкову стрічку, ідеальну для використання, як секретний ключ для Вашого нового сайту Django. Тепер ми вставимо цей ключ у файл `.env`, котрий Glitch покаже Вам, тільки якщо Ви є власником вебсайту.
> 
> - Створіть файл `.env` у корені вашого проєкту і додайте до нього наступну властивість:
>     
>     {% filename %}.env{% endfilename %}
>     
>     ```bash
>     # Тут, всередині одинарних лапок, ви можете вирізати та вставити випадковий ключ, згенерований вище
>     SECRET='3!0k#7ds5mp^-x$lqs2%le6v97h#@xopab&oj5y7d=hxe511jl'
>     
>     ```
> 
> - Потім оновіть файл параметрів Django, щоб ввести це секретне значення та встановити назву вебсайту Django:
>     
>     {% filename %}mysite/settings.py{% endfilename %}
>     
>     ```python
>     import os
>     
>     SECRET_KEY = os.getenv('SECRET')
>     ```
> 
> - І трохи далі в тому ж файлі ми вводимо назву вашого нового вебсайту Glitch:
>     
>     {% filename %}mysite/settings.py{% endfilename %}
>     
>     ```python
>     ALLOWED_HOSTS = [os.getenv('PROJECT_DOMAIN') + ".glitch.me"]
>     ```
>     
>     Значення `PROJECT_DOMAIN` автоматично генерується Glitch. Це буде відповідати назві Вашого проєкту.

## Створення бази даних

Існує безліч різноманітних програмних продуктів, що працюють із базами даних і можуть зберігати дані для вашого сайту. Ми будемо користуватися таким, що вказаний за замовчуванням - `sqlite3`.

Відповідні налаштування вже прописані у файлі `mysite/settings.py`:

{% filename %}mysite/settings.py{% endfilename %}

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```

Щоб створити базу даних для нашого блогу, давайте запустимо наступне в консолі: `python manage.py migrate` (ми повинні знаходитися всередині директорії `djangogirls`, яка містить файл `manage.py`). Якщо все пройшло успішно, ви маєте побачити щось на кшталт:

{% filename %}command-line{% endfilename %}

    (myvenv) ~/djangogirls$ python manage.py migrate
    Operations to perform:
      Apply all migrations: admin, auth, contenttypes, sessions
    Running migrations:
      Applying contenttypes.0001_initial... OK
      Applying auth.0001_initial... OK
      Applying admin.0001_initial... OK
      Applying admin.0002_logentry_remove_auto_add... OK
      Applying admin.0003_logentry_add_action_flag_choices... OK
      Applying contenttypes.0002_remove_content_type_name... OK
      Applying auth.0002_alter_permission_name_max_length... OK
      Applying auth.0003_alter_user_email_max_length... OK
      Applying auth.0004_alter_user_username_opts... OK
      Applying auth.0005_alter_user_last_login_null... OK
      Applying auth.0006_require_contenttypes_0002... OK
      Applying auth.0007_alter_validators_add_error_messages... OK
      Applying auth.0008_alter_user_username_max_length... OK
      Applying auth.0009_alter_user_last_name_max_length... OK
      Applying auth.0010_alter_group_name_max_length... OK
      Applying auth.0011_update_proxy_permissions... OK
      Applying auth.0012_alter_user_first_name_max_length... OK
      Applying sessions.0001_initial... OK
    

Ми це зробили! Час запустити веб сервер і перевірити чи працює наш сайт!

## Запуск вебсервера

Ви повинні знаходитися в папці, що містить файл `manage.py` (папка `djangogirls`). В консолі ми можемо активувати веб сервер запустивши `python manage.py runserver`:

{% filename %}command-line{% endfilename %}

    (myvenv) ~/djangogirls$ python manage.py runserver
    

Якщо Ви у Chromebook, скористайтеся краще цією командою:

{% filename %}Cloud 9{% endfilename %}

    (myvenv) ~/djangogirls$ python manage.py runserver 0.0.0.0:8080
    

Або цією, якщо Ви використовуєте Glitch:

{% filename %}Glitch.com terminal{% endfilename %}

    $ refresh
    
    

Якщо Ви використовуєте Windows і бачите помилку `UnicodeDecodeError`, слід виконати наступну команду:

{% filename %}command-line{% endfilename %}

    (myvenv) ~/djangogirls$ python manage.py runserver 0:8000
    

А зараз все, що ви повинні перевірити, це чи запущений ваш веб сайт. Відкрийте ваш браузер (Firefox, Chrome, Safari, Internet Explorer або будь-який інший) і введіть адресу:

{% filename %}browser{% endfilename %}

    http://127.0.0.1:8000/
    

Якщо ви використовуєте Chromebook і Cloud9, натомість натисніть на посилання у що спливає вікні, яке повинно було з'явитися у правому верхньому куті командного вікна, де працює вебсервер. Посилання буде виглядати приблизно так:

{% filename %}browser{% endfilename %}

    https://<a bunch of letters and numbers>.vfs.cloud9.us-west-2.amazonaws.com
    

Або на Glitch:

    https://name-of-your-glitch-project.glitch.me
    

Вітаємо! Ви щойно створили свій перший вебсайт та запустили його на вебсервері! Хіба ж це не круто?

![Встановлено!](images/install_worked.png)

Зверніть увагу, що вікно команд може виконувати тільки одну річ за раз, а вікно команд, що ви відкрили раніше запускає вебсервер. Поки вебсервер працює і чекає додаткових вхідних запитів, термінал прийме новий текст, але не бути виконувати нові команди.

> Ми розглянули як працюють вебсервери у розділі **How the Internet works**

Щоб ввести додаткові команди, поки працює вебсервер, відкрийте нове вікно терміналу та активуйте Ваше віртуальне середовище -- щоб переглянути інструкції, як відкрити друге вікно терміналу, дивіться [Introduction to the command line](../intro_to_command_line/README.md). Щоб зупинити вебсервер, перемикнутися назад до вікна, в якому він працює і натисніть CTRL+C - Control і C разом (на Windows, можливо доведеться натиснути Ctrl+Break).

Готові до наступного кроку? Час створювати контент!