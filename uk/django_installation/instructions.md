> Частина цього розділу базується на туторіалах Geek Girls Carrots (https://github.com/ggcarrots/django-carrots).
> 
> Частина цієї секції базується на матеріалі [django-marcador tutorial](http://django-marcador.keimlink.de/), який є ліцензованим Creative Commons Attribution-ShareAlike 4.0 International License. Авторське право на навчальні матеріали django-marcador tutorial належить Markus Zapke-Gründemann та ін.

## Віртуальне середовище

Перед тим як встановлювати Django, ми допоможемо вам встановити надзвичайно корисний інструмент, що допоможе підтримувати середовище розробки на вашому комп'ютері чистим. Цей крок можна пропустити, але дуже рекомендується його виконати. Починати найкращим можливим способом дозволить уникнути багатьох клопотів в майбутньому!

Отже, створимо віртуальне середовище (англ. **virtual environment** або скорочено *virtualenv*). Virtualenv ізолюватиме ваше Python/Django середовище, для кожного проекту. Це означає, що будь-які зміни, внесені на одному сайті не вплинуть на будь-які інші, які ви також розробляєте. Гарно, правда ж?

Все що вам необхідно зробити це знайти місце, де ви хочете створити віртуальне середовище `virtualenv`; наприклад, ваша домашня папка. На Windows, це може виглядати як `C:\Users\Name` (де `Name` є Вашим логіном).

> **ПРИМІТКА** на Windows, переконайтеся, що цей каталог не містить акцентованих або спеціальних символів; якщо ім'я користувача охоплює акцентовані символи, використайте інший каталог, наприклад, `C:\djangogirls`.

В рамках цього навчального посібника будемо використовувати нову директорію `djangogirls` з вашої домашньої папки:

{% filename %}command-line{% endfilename %}

    $ mkdir djangogirls
    $ cd djangogirls
    

Створимо віртуальне середовище з ім'ям `myvenv`. Загальна команда буде ось в такому форматі:

{% filename %}command-line{% endfilename %}

    $ python -m venv myvenv
    

<!--sec data-title="Virtual environment: Windows" data-id="virtualenv_installation_windows"
data-collapse=true ces-->

Щоб створити нове `віртуальне середовище`, потрібно відкрити командний рядок і запустити `python -m venv myvenv`. Це буде виглядати так:

{% filename %}command-line{% endfilename %}

    C:\Users\Name\djangogirls> python -m venv myvenv
    

Де `myvenv` являє собою назву вашого `віртуального середовища`</0>. Ви можете використовувати будь-яке ім’я, але старайтесь обмежитись маленькими буквами і не використовуйте пробілів, наголосів або спеціальних символів. Мати коротке ім'я - також гарна ідея, оскільки Ви будете часто посилатися на нього!

<!--endsec-->

<!--sec data-title="Virtual environment: Linux and OS X" data-id="virtualenv_installation_linuxosx"
data-collapse=true ces-->

Ми можемо створити `віртуальне середовище` як на Linux, так і на OS X, запускаючи `python3 -m venv myvenv`. Це буде мати такий вигляд:

{% filename %}command-line{% endfilename %}

    $ python -m venv myvenv
    

`myvenv` - ім'я вашого віртуального середовища `virtualenv`. Можете використовувати яке завгодно ім'я, але воно має містити лише маленькі літери і не містити пробілів. It is also a good idea to keep the name short as you'll be referencing it a lot!

> **ПРИМІТКА** У деяких версіях Debian/Ubuntu, Ви можете отримати таку помилку:
> 
> {% filename %}command-line{% endfilename %}
> 
>     The virtual environment was not created successfully because ensurepip is not available.  On Debian/Ubuntu systems, you need to install the python3-venv package using the following command.
>        apt install python3-venv
>     You may need to use sudo with that command.  After installing the python3-venv package, recreate your virtual environment.
>     
> 
> У такому випадку, дотримуйтесь наведених вище інструкцій і встановіть пакет `python3-venv`: {% filename %}command-line{% endfilename %}
> 
>     $ sudo apt install python3-venv
>     
> 
> **ПРИМІТКА** У деяких версіях Debian/Ubuntu створення такого віртуального середовища, призводить до наступної помилки:
> 
> {% filename %}command-line{% endfilename %}
> 
>     Error: Command '['/home/eddie/Slask/tmp/venv/bin/python3', '-Im', 'ensurepip', '--upgrade', '--default-pip']' returned non-zero exit status 1
>     
> 
> Щоб обійти цю проблему, використовуйте натомість команду `virtualenv`.
> 
> {% filename %}command-line{% endfilename %}
> 
>     $ sudo apt install python-virtualenv
>     $ virtualenv --python=python{{ book.py_version }} myvenv
>     
> 
> **ПРИМІТКА:** Якщо Ви отримаєте повідомлення про помилку, наприклад
> 
> {% filename %}command-line{% endfilename %}
> 
>     E: Unable to locate package python3-venv
>     
> 
> Після цього запустіть:
> 
> {% filename %}command-line{% endfilename %}
> 
>     sudo apt install python{{ book.py_version }}-venv
>     

<!--endsec-->

## Робота з віртуальним середовищем

Вищезазначена команда створить каталог під назвою `myvenv` (або інша вибрана Вами назва), що буде містити наше віртуальне середовище (в основному, набір каталогів і файлів).

<!--sec data-title="Working with virtualenv: Windows" data-id="virtualenv_windows"
data-collapse=true ces-->

Запустіть своє віртуальне середовище виконавши:

{% filename %}command-line{% endfilename %}

    C:\Users\Name\djangogirls> myvenv\Scripts\activate
    

> **ПРИМІТКА:** На Windows 10 Ви можете отримати помилку у Windows PowerShell, що повідомить `виконання скриптів на цій системі вимкнено`. У цьому випадку, відкрийте іншу опцію Windows PowerShell "Запуск від імені адміністратора". Потім спробуйте набрати наступну команду перед тим, як започаткувати ваше віртуальне середовище:
> 
> {% filename %}command-line{% endfilename %}
> 
>     C:\WINDOWS\system32> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
>         Execution Policy Change
>         The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose you to the security risks described in the about_Execution_Policies help topic at http://go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy? [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): A
>     

<!-- (This comment separates the two blockquote blocks, so that GitBook and Crowdin don't merge them into a single block.) -->

> **NOTE:** For users of the popular editor VS Code, which comes with an integrated terminal based off windows PowerShell, if you wish to stick with the integrated terminal, you may run the following command to activate your virtual environment:
> 
>     $ . myvenv\Scripts\activate.ps1
>     
> 
> Перевага в тому, що вам не потрібно перемикатися між вікнами редактора та вікнами командного рядка.

<!--endsec-->

<!--sec data-title="Working with virtualenv: Linux and OS X" data-id="virtualenv_linuxosx"
data-collapse=true ces-->

Запустіть своє віртуальне середовище виконавши:

{% filename %}command-line{% endfilename %}

    $ source myvenv/bin/activate
    

Не забудьте замінити `myvenv` на вибране Вами `віртуальне `ім'я!

> **ПРИМІТКА:** Якщо командне `джерело` не є доступним, спробуйте зробити замість цього це:
> 
> {% filename %}command-line{% endfilename %}
> 
>     $ . myvenv/bin/activate
>     

<!--endsec-->

Про активізацію віртуального середовища ви дізнаєтесь коли побачите підказку в командному рядку консолі, котра виглядатиме наступним чином.

When working within a virtual environment, `python` will automatically refer to the correct version so you can use `python` instead of `python3`.

OK, we have all important dependencies in place. We can finally install Django!

## Installing Django {#django}

Now that you have your `virtualenv` started, you can install Django.

Before we do that, we should make sure we have the latest version of `pip`, the software that we use to install Django:

{% filename %}command-line{% endfilename %}

    (myvenv) ~$ python -m pip install --upgrade pip
    

### Installing packages with requirements

A requirements file keeps a list of dependencies to be installed using `pip install`:

First create a `requirements.txt` file inside of the `djangogirls/` folder, using the code editor that you installed earlier. You do this by opening a new file in the code editor and then saving it as `requirements.txt` in the `djangogirls/` folder. Your directory will look like this:

    djangogirls
    ├── myvenv
    │   └── ...
    └───requirements.txt
    

In your `djangogirls/requirements.txt` file you should add the following text:

{% filename %}djangogirls/requirements.txt{% endfilename %}

    Django~={{ book.django_version }}
    

Now, run `pip install -r requirements.txt` to install Django.

{% filename %}command-line{% endfilename %}

    (myvenv) ~$ pip install -r requirements.txt
    Collecting Django~={{ book.django_version }} (from -r requirements.txt (line 1))
      Downloading Django-{{ book.django_version }}-py3-none-any.whl (7.9MB)
    Installing collected packages: Django
    Successfully installed Django-{{ book.django_version }}
    

<!--sec data-title="Installing Django: Windows" data-id="django_err_windows"
data-collapse=true ces-->

> If you get an error when calling pip on Windows, please check if your project pathname contains spaces, accents or special characters (for example, `C:\Users\User Name\djangogirls`). If it does, please consider using another place without spaces, accents or special characters (suggestion: `C:\djangogirls`). Create a new virtualenv in the new directory, then delete the old one and try the above command again. (Moving the virtualenv directory won't work since virtualenv uses absolute paths.)

<!--endsec-->

<!--sec data-title="Installing Django: Windows 8 and Windows 10" data-id="django_err_windows8and10"
data-collapse=true ces-->

> Your command line might freeze when you try to install Django. If this happens, instead of the above command use:
> 
> {% filename %}command-line{% endfilename %}
> 
>     C:\Users\Name\djangogirls> python -m pip install -r requirements.txt
>     

<!--endsec-->

<!--sec data-title="Installing Django: Linux" data-id="django_err_linux"
data-collapse=true ces-->

> If you get an error when calling pip on Ubuntu 12.04 please run `python -m pip install -U --force-reinstall pip` to fix the pip installation in the virtualenv.

<!--endsec-->

That's it! You're now (finally) ready to create a Django application!