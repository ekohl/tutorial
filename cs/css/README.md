# CSS - zkrášli svou stránku!

Náš blog nevypadá stále dost pěkně, že? Je na čase ho udělat hezčí! Použijeme na to CSS.

## Co je to CSS?

Kaskádové styly (Cascading Style Sheets, CSS) je jazyk používáný pro popis vzhledu a formátu webové stránky napsané ve značkovacím jazyce (jako například HTML). Berte to jako make-up pro naši webovou stránku. ;)

Ale nechceme začínat od nuly, že? Znovu použijeme něco, co už někdo vytvořil a umístil na Internet aby to mohli ostatní programátoři používat zdarma. Vymýšlení už vymyšlených věcí není zábava.

## Použijme Bootstrap!

Bootstrap je jeden z nejpopulárnějších frameworků pro HTML a CSS na vytváření krásných webových stránek: https://getbootstrap.com/

Byl vytvořen programátory, kteří pracovali pro Twitter. Nyní je Bootstrap vyvíjen dobrovolníky po celém světě!

## Instalace Bootstrapu

Pro instalaci Bootstrapu otevři svůj `.html` soubor v kódovém editoru a přidej tohle do `<head>` sekce:

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
```

Nepřidá to žádné soubory do tvého projektu. Jen to ukazuje na soubory, které existují na Internet. Takže do toho, otevři svoji webovou stránku a obnov ji. To je ono!

![Obrázek 14.1](images/bootstrap1.png)

Hned to vypadá lépe!

## Statické soubory v Djangu

Konečně se podíváme zblízka na téma, které jsme již zmínili, **statické soubory**. Statické soubory jsou všechna tvá CSS a obrázky. Jejich obsah nezávisí na kontextu požadavku a bude stejný pro každého uživatele.

### Kam umístit statické soubory pro Django

Django již ví, kde najít statické soubory pro vestavěnou "admin" aplikaci. Nyní potřebujeme přidat nějaké statické soubory do naší vlastní aplikace, `blog`.

Uděláš to tak, že vytvoříš složku s názvem `static` uvnitř aplikace blog:

    djangogirls
    ├── blog
    │   ├── migrations
    │   ├── static
    │   └── templates
    └── mysite
    

Django bude automaticky hledat jakékoliv složky nazvané "static" uvnitř tvých složek v aplikaci. Poté bude schopný použít jejich obsah jako statické soubory.

## Tvůj první soubor CSS!

Pojďme vytvořit nějaký CSS soubor a přidat vlastní styly pro tvou webovou stránku. Vytvoř nový adresář s názvem `css` uvnitř adresáře `static`. Vytvoř nový soubor s názvem `blog.css` uvnitř tohoto adresáře `css`. Připraveno?

    djangogirls
    └─── blog
         └─── static
              └─── css
                   └─── blog.css
    

Čas k napsání nějakého CSS! Otevři soubor `blog/static/css/blog.css` v editoru kódu.

Zde nebudeme zacházet příliš do detailů a učit se CSS nebo jej přizpůsobovat. Pokud se budeš chtít naučit více o CSS, na konci této stránky najdeš doporučení na CSS kurz zdarma.

Ale pojďme něco málo udělat. Možná bychom mohli změnit barvu našich nadpisů? Pro interpretaci barev, počítače používají speciální kódy. Tyto kódy začínají `#` a následuje 6 písmen(A-F) a číslic(0-9). Například kód pro modrou barvu bude vypadat takto: `#0000FF`. Kódy všech barev můžeš najít například zde: http://www.colorpicker.com/. Můžeš také použít [předdefinované barvy](http://www.w3schools.com/colors/colors_names.asp), `červená/red` a `zelená/green`.

V souboru `blog/static/css/blog.css` přidej následující kód:

{% filename %}blog/static/css/blog.css{% endfilename %}

```css
h1 a, h2 a {
    color: #C25100;
}

```

`h1` je CSS selector. Toto znamená, že aplikujeme naše styly na každý element `a` uvnitř elementu `h1` , selektor `h2` dělá to samé pro elementy `h2`. Takže když máme něco jako `<h1><a href="">odkaz</a></h1>`, použije se styl `h1`. V tomto případě říkáme, že barvu elementu měníme na `#C25100`, což je oranžová. Nebo zde můžeš vložit vlastní barvu, ale ujisti se, že bude kontrastní vůči bílé barvě pozadí stránky.

V CSS souboru určujeme styly pro prvky v souboru HTML. První způsob, jak identifikovat prvky je pomocí názvu elementu. Možná si vzpomeneš na tyto tagy ze sekce HTML. Věci jako `a`, `h1` a `body`jsou všechny příklady názvů elementů. Také identifikujeme elementy podle atributu `class` nebo atributu `id`. Třídy/Class a id jsou jména, které pojmenovávají samotný prvek. Třídy definují skupiny prvků a Id poukazují na konkrétní prvky. Například můžete určit následující prvek pomocí názvu prvku `a`, třída `external_link`nebo id `link_to_wiki_page`:

```html
<a href="https://en.wikipedia.org/wiki/Django" class="external_link" id="link_to_wiki_page">
```

Více si můžeš přečíst [CSS Selectoryna w3schools](http://www.w3schools.com/cssref/css_selectors.asp).

Pak je třeba také říct naší HTML šabloně, že jsme přidali nějaké CSS. Otevři soubor `blog/templates/blog/post_list.html` a přidej tento řádek na úplný začátek:

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
{% load static %}
```

Právě zde načítáme statické soubory. :) mezi značkami `<head>` a `</head>` , po odkazech na Bootstrap CSS soubory přidejte tento řádek:

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
<link rel="stylesheet" href="{% static 'css/blog.css' %}">
```

Prohlížeč čte soubory v pořadí, ve kterém jsou zadány, takže se musíme ujistit, že jsme na správném místě. V opačném případě může být kód v našem souboru přepsán kódem z Bootstrap souborů. Právě jsi řekla naší šabloně, kde je umístěn náš soubor CSS.

Soubor by měl nyní vypadat takto:

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
{% load static %}
<!DOCTYPE html>
<html>
    <head>
        <title>Django Girls blog</title>
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
        <link rel="stylesheet" href="{% static 'css/blog.css' %}">
    </head>
    <body>
        <header>
            <h1><a href="/">Django Girls Blog</a></h1>
        </header>

        {% for post in posts %}
            <article>
                <time>published: {{ post.published_date }}</time>
                <h2><a href="">{{ post.title }}</a></h2>
                <p>{{ post.text|linebreaksbr }}</p>
            </article>
        {% endfor %}
    </body>
</html>
```

OK, ulož soubor a aktualizuj stránky!

![Obrázek 14.2](images/color2.png)

Dobrá práce! Možná bychom také chtěli provzdušnit náš web a zvětšit okraj na levé straně? Pojďme to zkusit!

{% filename %}blog/static/css/blog.css{% endfilename %}

```css
body {
    padding-left: 15px;
}
```

Přidej toto do svého CSS souboru, ulož soubor a koukni se, jak to funguje!

![Obrázek 14.3](images/margin2.png)

Možná můžeme také chtít přizpůsobit písmo v našem záhlaví? Vlož mezi tag `< head >` v souboru `blog/templates/blog/post_list.html`:

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
<link href="//fonts.googleapis.com/css?family=Lobster&subset=latin,latin-ext" rel="stylesheet" type="text/css">
```

Stejně jako předtím, zkontroluj pořadí a místo před odkazem na `blog/static/css/blog.css`. Tento řádek importuje font s názvem *Lobster* z Google Fonts (https://www.google.com/fonts).

Najdi blok `h1 deklarací` (kód mezi závorkami `{` a `}`) v CSS souboru `blog/static/css/blog.css`. Nyní přidej řádek `font-family: 'Lobster';` mezi závorkami a obnov stránku:

{% filename %}blog/static/css/blog.css{% endfilename %}

```css
h1 a, h2 a {
    color: #C25100;
    font-family: 'Lobster';
}
```

![Obrázek 14.3](images/font.png)

Skvěle!

Jak bylo uvedeno výše, CSS má koncepci tříd. Ty ti umožňují pojmenovat část HTML kódu a aplikovat styly pouze na danou část, aniž by to ovlivnilo ostatní části. To může být super užitečné! Možná máš dva prvky 'div' , které dělají něco jiného (jako je hlavička a tvůj příspěvek). Třída ti může pomoci, aby element vypadal jinak.

Go ahead and name some parts of the HTML code. Replace the `header` that contains your header with the following:

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
<header class="page-header">
    <div class="container">
        <h1><a href="/">Django Girls Blog</a></h1>
    </div>
</header>
```

And now add a class `post` to your `article` containing a blog post.

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
<article class="post">
    <time>published: {{ post.published_date }}</time>
    <h2><a href="">{{ post.title }}</a></h2>
    <p>{{ post.text|linebreaksbr }}</p>
</article>
```

Nyní přidáme deklaraci bloků pro jiné selektory. Selektory začínající `.` se týkají tříd. Existuje mnoho skvělých návodů a vysvětlení CSS na webu, které ti pomohou pochopit následující kód. Pro tuto chvíli stačí zkopírovat a vložit do souboru `blog/static/css/blog.css`:

{% filename %}blog/static/css/blog.css{% endfilename %}

```css
.page-header {
    background-color: #C25100;
    margin-top: 0;
    margin-bottom: 40px;
    padding: 20px 20px 20px 40px;
}

.page-header h1,
.page-header h1 a,
.page-header h1 a:visited,
.page-header h1 a:active {
    color: #ffffff;
    font-size: 36pt;
    text-decoration: none;
}

h1,
h2,
h3,
h4 {
    font-family: 'Lobster', cursive;
}

.date {
    color: #828282;
}

.save {
    float: right;
}

.post-form textarea,
.post-form input {
    width: 100%;
}

.top-menu,
.top-menu:hover,
.top-menu:visited {
    color: #ffffff;
    float: right;
    font-size: 26pt;
    margin-right: 20px;
}

.post {
    margin-bottom: 70px;
}

.post h2 a,
.post h2 a:visited {
    color: #000000;
}

.post > .date,
.post > .actions {
    float: right;
}

.btn-secondary,
.btn-secondary:visited {
    color: #C25100;
    background: none;
    border-color: #C25100;
}

.btn-secondary:hover {
    color: #FFFFFF;
    background-color: #C25100;
}
```

Pak obklopující HTML kód, který zobrazuje příspěvek s deklaracemi tříd. Nahraď tímto:

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
{% for post in posts %}
    <article class="post">
        <time>published: {{ post.published_date }}</time>
        <h2><a href="">{{ post.title }}</a></h2>
        <p>{{ post.text|linebreaksbr }}</p>
    </article>
{% endfor %}
```

v `blog/templates/blog/post_list.html` tímto:

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
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
```

Tyto soubory ulož a aktualizuj své webové stránky.

![Obrázek 14.4](images/final.png)

Jupí! To je paráda, co? Podívej se na kód, který jsme právě vložili, abychom našli místa, kde jsme přidali třídy v HTML a používali je v CSS. Kde bys provedla změnu, pokud chceš, aby datum bylo tyrkysové?

Neboj se trochu pohrát s tímto CSS a pokus se některé věci změnit. Hraní s CSS ti pomůže pochopit, co dělají různé věci. Pokud něco rozbiješ, nedělej si starosti - vždy to můžeš vrátit zpět!

Opravdu doporučujeme vzít zdarma online kurzy "Základní HTML & HTML5" a "Základní CSS" na [freeCodeCamp](https://learn.freecodecamp.org/). Mohou ti pomoci naučit se, jak udělat tvé webové stránky hezčí pomocí HTML a CSS.

Připravena na další kapitolu?! :)