# Django URL

もうすぐ最初のWebページ、あなたのブログのホームページを作るところです！でも最初に、ちょっとだけDjangoのURLについて学びましょう。

## URLとは？

URLはWeb上のアドレスです。 サイトのURLは、ブラウザのアドレスバーで見ることができます。 （そう、 `127.0.0.1:8000` や `http://djangogirls.com` がURLです。）

![URL](images/url.png)

インターネット上のすべてのページには、独自のURLが必要です。 それによって、これから作るアプリケーションが、URLを指定してアクセスしてきたユーザに、何を見せたらいいのかわかるのです。 Djangoでは `URLconf`（URL設定）と呼ばれるものを使います。 URLconfはパターンの集まりで、適切なビューを見つけるために、DjangoがリクエストされたURLと照合するものです。

## DjangoでURLはどのように機能する？

`mysite/urls.py` を開いて、中身をみてみると：

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

ご覧のとおり、Djangoは既にこのようなものを置いてくれています。

三重クオート（ `'''` や `"""` ）で囲まれた行は、docstringとよばれるコメント行です。ファイル、クラス、またはメソッドの先頭に記述して、それが何をするかを説明するのに用います。 これはPythonによって実行されない行です。

前の章で訪れたadminのURLについてはすでに書いてありますね。

{% filename %}mysite/urls.py{% endfilename %}

```python
    path('admin/', admin.site.urls),
```

`admin/` で始まる全てのURLについて、Djangoが返すべき*ビュー*をこの行で指定しています。 今回の場合、adminで始まるURLをたくさん作ることになりますが、その全てをこの小さいファイルに書くようなことはしません。この方がきれいで読みやすいですし。

## あなたの初めてDjango URL!

さあ最初のURLを作りましょう！'http://127.0.0.1:8000/' をブログの入口ページにして、ブログの投稿のリストを表示するようにしたいと思います。

`mysite/urls.py` ファイルは簡潔なままにしておきたいので、`mysite/urls.py` では`blog` アプリからURLをインポートするだけにしましょう。

まず、`blog.urls` をインポートする行を追加しましょう。 ここで、`include`関数を使いたいので、`from django.urls…`の行を変更し、そのインポートを追加する必要があります。

`mysite/urls.py` ファイルはこのようになります：

{% filename %}mysite/urls.py{% endfilename %}

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('blog.urls')),
]
```

これでDjangoは'http://127.0.0.1:8000/' に来たリクエストは `blog.urls` へリダイレクトするようになり、それ以降はそちらを参照するようになります。

## blogのURL

`blog` ディレクトリの下に、新しく `urls.py` という空のファイルを作って、コードエディタで開いて下さい。そして最初の2行を以下のように書きます：

{% filename %}blog/urls.py{% endfilename %}

```python
from django.urls import path
from . import views
```

これはDjangoの `path` 関数と、`blog` アプリの全ての `ビュー`（といっても、今は一つもありません。すぐに作りますけど！）をインポートするという意味です。

その後、最初のURLパターンを追加します。

{% filename %}blog/urls.py{% endfilename %}

```python
urlpatterns = [
    path('', views.post_list, name='post_list'),
]
```

見てのとおり、`post_list` という名前の `ビュー` をルートURLに割り当てています。 このURLパターンは空の文字列に一致します。Djangoはビューを見つけるとき、URLのパス(path)の前にくっつくドメイン名（つまり、http://127.0.0.1:8000/ の部分）を無視します。 このパターンは誰かがあなたのWebサイトの 'http://127.0.0.1:8000/' というアドレスにアクセスしてきたら `views.post_list` が正しい行き先だということをDjangoに伝えます。

最後の `name='post_list'` は、ビューを識別するために使われるURL の名前です。 これはビューと同じ名前にすることもできますが、全然別の名前にすることもできます。 プロジェクトでは名前づけされたURLを後で使うことになるので、アプリのそれぞれのURLに名前をつけておくのは重要です。また、URLの名前はユニークで覚えやすいものにしておきましょう。

もし今 http://127.0.0.1:8000/ にアクセスしたら、'web page not available' のようなメッセージが出るでしょう。 これはサーバー（ `runserver` ってタイプしたのを覚えていますか？）が動いていないからです。 なぜこうなったのかを知るためにサーバーのコンソール画面を見てみましょう。

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
    

エラーが表示されていますね。でも心配しないで。これはむしろ、結構便利なものなんですよ：ここでは、**'post_list' という属性(attribute)がない**ことを知らせてくれています。 これは *ビュー* の名前で、Djangoが探して使おうとしましたが、私たちはこれをまだ作っていませんでした。 現時点では、`/admin/` も動作していないと思います。 心配しなくて大丈夫です。ちゃんとできますから。 別のエラーメッセージが表示された場合は、Webサーバーを再起動してみてください。 これを行うには、Webサーバーを実行しているコンソールウィンドウで、Ctrl + C（CtrlキーとCキーを同時に押す）で停止します。 Windowsの場合、Ctrl + Breakかもしれません。 その後、`python manage.py runserver`を実行してWebサーバーを再起動します。

> If you want to know more about Django URLconfs, look at the official documentation: https://docs.djangoproject.com/en/3.2/topics/http/urls/