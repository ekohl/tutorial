# Розширення шаблону

Інша хороша річ, яку має Django у своєму арсеналі це **шаблонне розширення**. Що це означає? А це означає, що ви можете використовувати одні й ті ж частини свого HTML коду для різних сторінок вебсайту.

Шаблони допомагають коли ви хочете використати одну і ту ж інформацію чи макет у більш ніж одному місці. Ви можете не повторюватись у кожному файлі. І якщо ви хочете щось змінити, не потрібно робити це в кожному шаблоні, лише в одному!

## Створення базового шаблону

Базовий шаблон - це основний шаблон, який ви будете розширювати для кожної сторінки вашого вебсайту.

Створимо файл `base.html` в `blog/templates/blog/`:

    blog
    └───templates
        └───blog
                base.html
                post_list.html
    

Тепер відкрийте його і скопіюйте усе з `post_list.html` до файлу `base.html`, як тут:

{% filename %}blog/templates/blog/base.html{% endfilename %}

```html
{% load static %}
<!DOCTYPE html>
<html>
    <head>
        <title>Django Girls blog</title>
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
        <link href='//fonts.googleapis.com/css?family=Lobster&subset=latin,latin-ext' rel='stylesheet' type='text/css'>
        <link rel="stylesheet" href="{% static 'css/blog.css' %}">
    </head>
    <body>
        <header class="page-header">
          <div class="container">
              <h1><a href="/">Django Girls Blog</a></h1>
          </div>
        </header>

        <main class="container">
            <div class="row">
                <div class="col">
                {% for post in posts %}
                    <article class="post">
                        <time class="date">
                            {{ post.published_date }}
                        </time>
                        <h2><a href="">{{ post.title }}</a></h2>
                        <p>{{ post.text|linebreaksbr }}</p>
                    </article>
                {% endfor %}
                </div>
            </div>
        </main>
    </body>
</html>
```

Далі в `base.html`, замініть весь вміст `<body>` (все між `<body>` і `</body>`) на це:

{% filename %}blog/templates/blog/base.html{% endfilename %}

```html
<body>
    <header class="page-header">
      <div class="container">
          <h1><a href="/">Django Girls Blog</a></h1>
      </div>
    </header>
    <main class="container">
        <div class="row">
            <div class="col">
            {% block content %}
            {% endblock %}
            </div>
        </div>
    </main>
</body>
```

{% raw %}Ви могли помітити, що замінилось все від `{% for post in posts %}` до `{% endfor %}` на це: {% endraw %}

{% filename %}blog/templates/blog/base.html{% endfilename %}

```html
{% block content %}
{% endblock %}
```

Але навіщо? Ви щойно створили `block`! Ви використали тег шаблону `{% block %}`, щоб зробити область, в яку буде введений HTML. Цей HTML буде взятий з іншого шаблону, який розширить шаблон `base.html`. Скоро ми покажемо вам як це зробити.

Тепер збережіть `base.html` і знову відкрийте ваш `blog/templates/blog/post_list.html` в редакторі коду. {% raw %}Вам треба видалити все перед `{% for post in posts %}` та після `{% endfor %}`. Коли ви закінчите, файл буде виглядати так:{% endraw %}

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
{% for post in posts %}
    <article class="post">
        <time class="date">
            {{ post.published_date }}
        </time>
        <h2><a href="">{{ post.title }}</a></h2>
        <p>{{ post.text|linebreaksbr }}</p>
    </article>
{% endfor %}
```

Ми хочемо використати це як частину нашого шаблону для всіх блоків контенту. Час додати теги блоків до цього файлу!

{% raw %}Ви хочете, щоб ваш тег блоку відповідав тегу у файлі `base.html`. Ви також хочете включити весь код, який треба до ваших блоків контенту. Для цього вставте все між `{% block content %}` та `{% endblock %}`. Наступним чином:{% endraw %}

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
{% block content %}
    {% for post in posts %}
        <article class="post">
            <time class="date">
                {{ post.published_date }}
            </time>
            <h2><a href="">{{ post.title }}</a></h2>
            <p>{{ post.text|linebreaksbr }}</p>
        </article>
    {% endfor %}
{% endblock %}
```

Залишилося лише одне. Нам необхідно з'єднати ці два шаблони разом. Це і є розширення шаблону! Ми зробимо це, додавши додатковий тег до початку файлу. Як тут:

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
{% extends 'blog/base.html' %}

{% block content %}
    {% for post in posts %}
        <article class="post">
            <time class="date">
                {{ post.published_date }}
            </time>
            <h2><a href="">{{ post.title }}</a></h2>
            <p>{{ post.text|linebreaksbr }}</p>
        </article>
    {% endfor %}
{% endblock %}
```

Ось і все! Збережіть файл, та перевірте чи ваш сайт все ще працює належним чином. :)

> Якщо з'явилась помилка `TemplateDoesNotExist`, то це означає що відсутній файл `blog/base.html` і у вас запущений `runserver` в консолі. Спробуйте зупинити його (натиснувши Ctrl+C – клавіші Control та C разом) та перезавантажте його, запустивши команду `python manage.py runserver`.