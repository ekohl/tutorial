# URL-e Django

Zaczynamy budować naszą pierwszą stronę internetową: będzie to miejsce dla twojego bloga! Ale zanim zaczniemy, nauczmy się trochę na temat URL-i w Django.

## Czym jest URL?

Adres URL to adres w internecie. Możesz zobaczyć URL-a za każdym razem, gdy odwiedzasz stronę internetową - jest on widoczny w pasku adresu przeglądarki internetowej. (Tak! `127.0.0.1:8000` jest adresem URL! Też `https://djangogirls.org` jest adresem URL.)

![URL](images/url.png)

Każda strona w internecie potrzebuje własnego adresu URL. W ten sposób aplikacja wie, co wyświetlić użytkownikowi, który otworzy dany URL. W Django używamy tak zwanego `URLconf` (konfiguracji URL). URLconf to zestaw wzorców, które Django spróbuje dopasować do żądanego adresu URL, aby znaleźć poprawny widok.

## Jak działają adresy URL w Django?

Otwórzmy plik `mysite/urls.py` i przyjrzyjmy się jego treści:

{% filename %}mysite/urls.py{% endfilename %}

```python
"""mysite URL Configuration

[...]
"""
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

Jak zauważyłaś, Django coś nam już tu umieścił.

Linie między potrójnymi cudzysłowami (` '''` lub `""" `) nazywa się docstrings - możesz zapisać je na górze pliku, klasy lub metody, aby opisać, co robi. Nie będą one uruchamiane przez Pythona.

Adres URL panelu administracyjnego, który odwiedzałaś w poprzednim rozdziale, jest już tutaj dodany:

{% filename %}mysite/urls.py{% endfilename %}

```python
    path('admin/', admin.site.urls),
```

To znaczy, że dla każdego adresu zaczynającego się od `admin/` Django spróbuje dopasować odpowiedni *widok*. W tym przypadku używamy wielu adresów URL panelu administracyjnego, dlatego nie wypisujemy ich wszystkich w tym jednym małym pliku - tak jest czytelniej i bardziej estetycznie.

## Twój pierwszy adres URL w Django!

Czas utworzyć nasz pierwszy adres URL! Chcemy, aby adres 'http://127.0.0.1:8000/' był stroną główną naszego bloga i wyświetlał listę wpisów.

Zależy nam również, aby zachować porządek w pliku `mysite/urls.py`, dlatego zaimportujemy URL-e z naszej aplikacji `blog` do głównego pliku `mysite/urls.py`.

Śmiało, dodaj linię, która spowoduje zaimportowanie `blog.urls`. Będziesz musiała także zmienić pierwszy wiersz ` from django.urls...`, ponieważ użyjemy tutaj funkcji `include`, którą musimy najpierw zaimportować.

Twój plik `mysite/urls.py` powinien teraz wyglądać tak:

{% filename %}mysite/urls.py{% endfilename %}

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('blog.urls')),
]
```

Django przekieruje wszystkie reguły z adresu 'http://127.0.0.1:8000/' do `blog.urls` i tam będzie szukał dalszych wskazówek.

## blog.urls

Stwórz nowy pusty plik o nazwie `urls.py` w katalogu `blog` i otwórz go w Twoim edytorze. Dokładnie tak! Dodaj te pierwsze dwie linie:

{% filename %}blog/urls.py{% endfilename %}

```python
from django.urls import path
from . import views
```

Tutaj importujemy funkcje `path` Django i wszystkie nasze widoki (`views`) z aplikacji `blog`. (Nie mamy jeszcze żadnych, ale do tego dojdziemy za chwilę!)

Potem możemy dodać nasz pierwszy wzorzec adresu URL:

{% filename %}blog/urls.py{% endfilename %}

```python
urlpatterns = [
    path('', views.post_list, name='post_list'),
]
```

Jak widzisz, teraz przyporządkowujemy widok (`view`) o nazwie `post_list` do strony głównej. This URL pattern will match an empty string and the Django URL resolver will ignore the domain name (i.e., http://127.0.0.1:8000/) that prefixes the full URL path. Ten wzorzec będzie wskazówką dla Django, że `views.post_list` jest właściwym miejscem dla każdego, kto wejdzie na stronę poprzez adres 'http://127.0.0.1:8000/'.

Ostatnia część, `name='post_list` jest nazwą URL, która będzie używana do zidentyfikowania widoku. Nazwa może być taka sama jak nazwa widoku albo kompletnie inna. W projekcie będziemy później używać nazw URL, więc ważne jest nazwanie każdego URL-a w aplikacji. Powinnyśmy również starać się używać nazw URL unikalnych i prostych do zapamiętania.

Jeśli teraz spróbujesz odwiedzić stronę http://127.0.0.1:8000/, zobaczysz komunikat "niedostępna strona internetowa". Wynika to z faktu, że serwer (pamiętałaś o wpisaniu ` runserver`?) nie jest już uruchomiony. Spójrz na okno konsoli serwera, aby dowiedzieć się, dlaczego.

{% filename %}{{ warning_icon }} command-line{% endfilename %}

        return _bootstrap._gcd_import(name[level:], package, level)
      File "<frozen importlib._bootstrap>", line 1030, in _gcd_import
      File "<frozen importlib._bootstrap>", line 1007, in _find_and_load
      File "<frozen importlib._bootstrap>", line 986, in _find_and_load_unlocked
      File "<frozen importlib._bootstrap>", line 680, in _load_unlocked
      File "<frozen importlib._bootstrap_external>", line 850, in exec_module
      File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
      File "/Users/ola/djangogirls/blog/urls.py", line 5, in <module>
        path('', views.post_list, name='post_list'),
    AttributeError: module 'blog.views' has no attribute 'post_list'
    

Twoja konsola pokazuje błąd, ale nie martw się - w rzeczywistości jest to całkiem użyteczne: mówi Ci, że** brak atrybutu 'post_list'**. To jest nazwa widoku (*view*), którą Django próbuje znaleźć i użyć, ale jeszcze go nie utworzyłyśmy. Na tym etapie Twój `/admin/ ` również nie będzie działać. Nie martw się, zajmiemy się tym. Jeżeli pojawiła Ci się wiadomość o innym błędzie, spróbuj zrestartować swój serwer. To do that, in the console window that is running the web server, stop it by pressing Ctrl+C (the Control and C keys together). On Windows, you might have to press Ctrl+Break. Then you need to restart the web server by running a `python manage.py runserver` command.

> If you want to know more about Django URLconfs, look at the official documentation: https://docs.djangoproject.com/en/3.2/topics/http/urls/