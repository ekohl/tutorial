Ви можете [перейти у цей розділ](http://tutorial.djangogirls.org/en/installation/#install-python), якщо ви не використовуєте Chromebook. Якщо ви використовуєте Chromebook, процес встановлення може відрізнятись. Ви можете ігнорувати інші інструкції з установки.

### Cloud IDE (PaizaCloud Cloud IDE, AWS Cloud9, Glitch.com)

Cloud IDE це інструмент який надає вам редактор коду та доступ до комп'ютера в мережі Інтернет де ви можете встановлювати, писати та запускати програми. Протягом курсу, сloud IDE буде виконувати функцію вашого *локального ком'ютера*. Ви будете запускати команди в терміналі як і ваші одногрупники на OS X, Ubuntu або Windows, але ваш термінал буде керувати комп'ютером виділеним для вас Cloud IDE. Тут ви знайдете інструкції для Cloud IDEs (PaizaCloud Cloud IDE, AWS Cloud9, Glitch.com). Ви можете обрати одне з cloud IDE і використовувати інструкції для нього.

#### PaizaCloud Cloud ID

1. Перейдіть на [PaizaCloud Cloud IDE](https://paiza.cloud/)
2. Зареєструйте обліковий запис
3. Клацніть«*New Server*» і оберіть «Django app»
4. Натисніть на кнопку Terminal (в лівій частині вікна)

Тепер ви маєте побачити інтерфейс з боковою панеллю так кнопками зліва. Натисніть кнопку Terminal щоб відкрити вікно терміналу з наступним виводом:

{% filename %}Terminal{% endfilename %}

    $
    

Термінал на PaizaCloud IDE готовий до ваших інструкцій. Ви можете змінити розмір або максимізувати це вікно, щоб зробити його трохи більшим.

#### AWS Cloud9

В даний час Cloud 9 вимагає зареєструватися за допомогою AWS і ввести інформацію кредитної карти.

1. Встановити Cloud 9 з [веб-магазину Chrome](https://chrome.google.com/webstore/detail/cloud9/nbdmccoknlfggadpfkmcpnamfnbkmkcp)
2. Перейдіть до [c9.io](https://c9.io) та натисніть *Get started with AWS Cloud9*
3. Створіть обліковий запис AWS (потрібна інформація про кредитну картку, але ви можете користуватись цим безкоштовно)
4. В AWS-Dashboard, введіть *Cloud9* в рядку пошуку і клацніть на ньому
5. У панелі Cloud9 натисніть *Create environment*
6. Назвіть його *django-girls*
7. Під час налаштування параметрів виберіть *Create a new instance for environment (EC2)* для "Environment Type" та *t2.micro* для "Instance type" (він має сказати "Free-tier eligible."). Економне налаштування за замовчуванням задовільне, а ви можете залишити інші значення також без змін.
8. Натисніть *Next step*
9. Натисніть *Create environment*

Тепер ви повинні побачити інтерфейс із бічною панеллю, великим основним вікном з деяким текстом, і маленьке вікно внизу, що виглядає приблизно так:

{% filename %}bash{% endfilename %}

    yourusername:~/workspace $
    

Ця нижня область є вашим терміналом. Ви можете використовувати термінал, щоб відправляти інструкції на віддалений комп'ютер Cloud9. Ви можете змінити розмір вікна, щоб зробити його трохи більшим.

#### Glitch.com хмара IDE

1. Перейдіть на Glitch.com
2. Зареєструйтесь за обліковим записом ( https://glitch.com/signup) або використовуйте акаунт GitHub, якщо маєте. (Дивіться інструкцію до GitHub нижче)
3. Натисніть Новий проект та оберіть Головна сторінка
4. Натисніть на випадаючому списку інструментів (внизу лівої сторони вікна) , потім натисніть на конпку терміналу , щоб відкрити закладку командного рядка таким чином:

{% filename %} Термінал {% endfilename %}

    Програма@ ім'я твого проекту
    

Тобі не потрібно створювати віртуальне середовище при використанні Glitch.com як Ваш Cloud.IDE

{% filename %}glitch.json{% endfilename %}

```json
{
  "install": "pip3 install -r requirements.txt --user",
  "start": "bash start.sh",
  "watch": {
    "throttle": 1000
  }
}
```

{% filename %}requirements.txt{% endfilename %}

    Django~={{ book.django_version }}
    

{% filename %}.bash_profile{% endfilename %}

```bash
alias python=python3
alias pip=pip3
```

{% filename %}start.sh{% endfilename %}

```bash
chmod 600 .bash_profile
pip3 install -r requirements.txt --user
python3 manage.py makemigrations
python3 manage.py migrate
python3 manage.py runserver $PORT
```

Once these files are created, go to the Terminal and execute the following commands to create your first Django project:

{% filename %}Terminal{% endfilename %}

    django-admin.py startproject mysite .
    refresh
    

In order to see detailed error messages, you can activate Django debug logs for your Glitch application. Simply add the following at the end of the `mysite/settings.py` file.

{% filename %}mysite/settings.py{% endfilename %}

```python
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'handlers': {
        'file': {
            'level': 'DEBUG',
            'class': 'logging.FileHandler',
            'filename': 'debug.log',
        },
    },
    'loggers': {
        'django': {
            'handlers': ['file'],
            'level': 'DEBUG',
            'propagate': True,
        },
    },
}
```

This will create a `debug.log` file detailing Django operations and any error messages that might come up, making it much easier to fix if your website does not work.

The initial restarting of the Glitch project should fail. (If you click on the top dropdown button `Show` then click on `In a New Window`, you will receive a `DisallowedHost` error message.) Do not worry about it at this stage, the tutorial will fix this as soon as you update the Django settings of your project in the `mysite/settings.py` file.

### Віртуальне середовище

Віртуальне середовище (також зване virtualenv) - це як приватна скриня, яку ми можемо наповнювати корисним комп'ютерним кодом для проекту, над яким ми працюємо. Ми використовуємо їх для зберігання різноманітних частин коду, які потрібні нам для різних проєктів як окремі частини, так щоб не було плутанини між проєктами.

Запуск:

{% filename %}Cloud 9{% endfilename %}

    mkdir djangogirls
    cd djangogirls
    python3 -m venv myvenv
    source myvenv/bin/activate
    pip install django~={{ book.django_version }}
    

(зверніть увагу на те що в останньому рядку ми використовуємо знак тильди слідом за яким йде знак рівності:`~=`).

### GitHub

Створіть [GitHub](https://github.com) обліковий запис.

### PythonAnywhere

Посібник Django Girls містить розділ по так званому Розгортанні, що є процесом отримання коду, який забезпечує роботу вашого нового веб-додатка і переміщення його на загальнодоступний комп’ютер (так званий сервер), отож люди можуть бачити вашу роботу.

Ця частна є трохи дивною в навчанні по Chromebook, оскільки ми вже використовуємо комп'ютер, який знаходиться в Інтернеті (на відміну від, скажімо, ноутбука). Однак, це все ще корисно, оскільки ми можемо розглядати нашу робочий простір Cloud 9 як місце для нашої роботи "в процесі" і Python Anywhere як місце, де можна показати наші речі,коли вони стають більш завершеними.

Таким чином, зареєструйте новий обліковий запис Python Anywhere на [www.pythonanywhere.com](https://www.pythonanywhere.com).