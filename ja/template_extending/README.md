# テンプレートを拡張しよう

Djangoのまた別の素敵なところは**テンプレート拡張**です。これは何を意味するのでしょうか？それはHTMLの共通部分をウェブサイトの異なるページで使えるということです。

テンプレートは同じ情報やレイアウトを複数の場所で利用したいときに役立ちます。 各ファイル内で繰り返す必要はありません。 さらにもし何か変更したい場合、各テンプレートを変更する必要はなく、1回変更すればいいだけです！

## 基本テンプレートを作成する

基本テンプレートはあなたのウェブサイトの各ページを拡張するための最も基本的なテンプレートです。

`blog/templates/blog/`以下に`base.html`ファイルを作ってみましょう。

    blog
    └───templates
        └───blog
                base.html
                post_list.html
    

それからエディタで開いて、以下のように`post_list.html`から`base.html`ファイルにすべてコピーしましょう。

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

それから`base.html`内の`<body>`全体(`<body>`と`</body>`の間のすべて)を次で置き換えます。

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

{% raw %}`{% for post in posts %}` から `{% endfor %}` が以下のように置き換えられたことに気づいたでしょうか。 {% endraw %}

{% filename %}blog/templates/blog/base.html{% endfilename %}

```html
{% block content %}
{% endblock %}
```

でも何のために？ あなたはただ`block`を作っただけです！ `{% block %}` テンプレートタグを、これからHTMLを挿入しようとする場所に使いました。 そのHTMLはこのテンプレート (`base.html`) を拡張した別のテンプレートからやってきます。 どうやって行うかはすぐに示します。

`base.html`を保存し、もう一度`blog/templates/blog/post_list.html`をエディタで開きます。 {% raw %} `{% for post in posts %}` の上と `{% endfor %}` の下すべてを削除しましょう。 それが終わったら以下のようになっていると思います。{% endraw %}

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

これをcontentブロックに対応するテンプレートのパーツとして使いたいです。このファイルにblockタグを追加する時です！

{% raw %}追加するblockタグは `base.html` ファイル中のタグにマッチしてほしいですよね。 また、blockタグにはcontentブロックに属するすべてのコードを含めたいですよね。 そうするには、すべてを `{% block content %}` と `{% endblock %}` の間に入れてあげればよいです。 このように:{% endraw %}

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

あとやることは一つだけです。これら二つのテンプレートをくっつけてあげる必要があります。これがテンプレートを拡張するということのすべてです！そうするにはこのファイルの先頭にextendsタグを追加します。次のように：

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

以上です！ファイルを保存して、ウェブサイトがまだちゃんと動いているか確認しましょう。:)

> もし `TemplateDoesNotExist` というエラーが出ていたら、 `blog/base.html` ファイルがないという意味で、コンソールで `runserver` が実行されたままになっていると思います。 これを止め(Ctrl+C - ControlとCのキーを同時押し)、それから `python manage.py runserver`コマンドを入力して再度サーバーを動かしてみてください。