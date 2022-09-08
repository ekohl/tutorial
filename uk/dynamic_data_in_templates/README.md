# Динамічні дані в шаблонах

Маємо різні шматочки на своїх місцях: модель `Post` визначено в `models.py`, маємо `post_list` у `views.py`, а також відповідний шаблон. Однак, яким чином ми змусимо наші пости з'явитися в HTML шаблоні? Оскільки це те, що ми хочемо зробити – взяти деякий контент (моделі, збережені в базі даних) і відобразити його в гарному вигляді в нашому шаблоні, чи не так?

Це саме те, що покликані робити відображення: з'єднаємо моделі і шаблони. У нашому `post_list` *view* нам потрібно буде взяти моделі, які ми хочемо відобразити, і перенести їх у шаблон. У *view* ми вирішуємо, що (модель) буде відображатися в шаблоні.

Добре, як же ми цього досягнемо?

Нам потрібно відкрити наш `blog/views.py` у нашому редакторі коду. Таким чином, `post_list` *view* виглядає так:

{% filename %}blog/views.py{% endfilename %}

```python
from django.shortcuts import render

def post_list(request):
    return render(request, 'blog/post_list.html', {})
```

Пам'ятаєте як ми говорили про включення коду написаного в різних файлах? Настав момент, коли ми повинні включити модель, яку ми написали в `models.py`. Додамо рядок `з .models import Post` так:

{% filename %}blog/views.py{% endfilename %}

```python
from django.shortcuts import render
from .models import Post
```

Крапка перед `models` означає *поточний каталог* або *поточний додаток*. Обидві функції `views.py` і `models.py` знаходяться в одному каталозі. Це означає, що ми можемо використовувати `.` і ім’я файлу (без `.py`). Далі ми імпортуємо ім'я моделі (`Post`).

Але що далі? Щоб вилучити реальні дописи блогу з моделі `Post`, нам потрібно дещо під назвою `QuerySet`.

## QuerySet

Ви вже повинні бути ознайомлені з тим, як працюють QuerySets. Ми говорили про них у [розділі Django ORM (QuerySets)](../django_orm/README.md).

Отже, тепер ми хочемо, щоб опубліковані дописи в блозі були відсортовані за `датою_публікування`, чи не так? Ми вже робили це в розділі QuerySets!

{% filename %}blog/views.py{% endfilename %}

```python
Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
```

Отже, давайте відкриємо файл `blog/views.py` у редакторі коду та додамо цей фрагмент коду до функції `def post_list(request)`, але не забудьте спочатку додати `часовий пояс імпорту з django.utils`:

{% filename %}blog/views.py{% endfilename %}

```python
from django.shortcuts import render
from django.utils import timezone
from .models import Post

def post_list(request):
    posts = Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
    return render(request, 'blog/post_list.html', {})
```

Щоб відобразити наш QuerySet у нашому списку публікацій у блозі, нам залишилося зробити дві речі:

1. Перенесіть QuerySet `posts` до контексту шаблону, змінивши виклик функції `render`. Ми зараз це зробимо.
2. Змініть шаблон, щоб відобразити `публікації` QuerySet. Ми розглянемо це в наступному розділі.

Зазначте, будь ласка, що ми створюємо *змінну* для нашого QuerySet: `posts`. Сприймайте її як ім'я для QuerySet. З цього моменту ми можемо посилатися на неї через це ім'я.

У функції `render` у нас є один параметр `request` (все, що ми отримуємо від користувача через Інтернет) і інший, що надає шаблону файл (`'blog/post_list.html '`). Останній параметр, `{}`, є місцем, куди ми можемо додати певні речі, які шаблон може використовувати. Ми повинні дати їм імена (ми обмежились ім'ям `'posts'` наразі). :) Це має виглядати як: `{'posts': posts}`. Зверніть увагу, що частина перед `:` є рядком; Вам потрібно взяти цю частину в лапки: `''`.

Отже, врешті-решт наш файл `blog/views.py` матиме наступний вигляд:

{% filename %}blog/views.py{% endfilename %}

```python
from django.shortcuts import render
from django.utils import timezone
from .models import Post

def post_list(request):
    posts = Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
    return render(request, 'blog/post_list.html', {'posts': posts})
```

Це все! Час повернутись назад до нашого шаблону і вивести QuerySet!

Want to read a little bit more about QuerySets in Django? You should look here: https://docs.djangoproject.com/en/3.2/ref/models/querysets/