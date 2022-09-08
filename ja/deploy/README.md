# デプロイ！

> **補足** このチャプターはちょっと難しいことが沢山書かれています。 頑張って最後までやりきってください。デプロイはウェブサイトを開発するプロセスの上で、とても重要な部分ですが、つまずきやすいポイントも多く含まれています。 チュートリアルの途中にこのチャプターを入れています。そういったつまずきやすい箇所はメンターに質問して、あなたが作っているウェブサイトをオンラインでみれるようにしてください。 言い換えれば、もし時間切れでワークショップ内でチュートリアルを終わらせることができなかったとしても、この後のチュートリアルはきっと自分で終わらせることができるでしょう。

今のところ、あなたが作ったサイトは、あなたのコンピューターでしかみることができません。 ここでは、デプロイの方法を学びましょう！ デプロイとは、あなたが作っているアプリケーションをインターネットで公開することです。あなた以外の人もウェブサイトを見ることができるようになりますよ. :)

これまでに学んだとおり、ウェブサイトはサーバーに置かれています。 インターネットで利用できる多くのサーバー プロバイダーがありますが、私達は [PythonAnywhere](https://www.pythonanywhere.com/) を使用します。 PythonAnywhere は、多くの人がアクセスするものではない小さいアプリケーションを無料で公開できますので今のあなたには最適でしょう。

使用するその他の外部サービスは [GitHub](https://www.github.com)、コードのホスティング サービスです。 他にも色々ありますが、ほとんどのプログラマはGitHubのアカウントを持っています。そしてあなたも今そうなります。

これら3つの場所が重要になります。 ローカルコンピューターは、開発およびテストを行う場所になります。 変更に満足したら、GitHub上にプログラムのコピーを配置します。 あなたのウェブサイトはPythonAnywhereで公開され、GitHub からコードの新しいコピーを取得することによって更新されます。

# Git

> **注意** もしすでに[インストール手順](../installation/README.md)を行っていた場合は、このステップを再び行う必要はありません。次のステップにスキップして Git リポジトリを作り始めてください。

{% include "/deploy/install_git.md" %}

## Gitリポジトリを始める

Gitはコードリポジトリ（または略して「リポジトリ」）というものの中に置かれる特定のファイルへの変更を追跡します。 私たちのプロジェクトを開始しましょう。 あなたのコンソールを開き、`djangogirls` ディレクトリでこれらのコマンドを実行します。

> **備考：**リポジトリを初期化する前に `pwd` (OSX/Linux) または `cd` (Windows) コマンドで現在の作業ディレクトリを確認してください。 `djangogirls` フォルダー内にいる必要があります。

{% filename %}command-line{% endfilename %}

    $ git init
    Initialized empty Git repository in ~/djangogirls/.git/
    $ git config --global user.name "Your Name"
    $ git config --global user.email you@example.com
    

gitリポジトリを初期化することは、プロジェクトごとに1回だけ行う必要があります（ユーザー名と電子メールをもう一度入力する必要はありません）。

### ブランチ名の調整

使用しているGitのバージョンが **2.28** よりも古い場合は、ブランチの名前を「main」に変更する必要があります。 Gitのバージョンを調べるには、以下のコマンドを入力してください。

{% filename %}command-line{% endfilename %}

    $ git --version
    git version 2.xx...
    

上記のように「xx」と表示されているバージョンの2番目の数が28未満の場合のみ、ブランチの名前を変更するために次のコマンドを入力する必要があります。 28以上の場合は「無視するファイル」へ続いてください。 As in "Initializing", this is something we need to do only once per project, as well as only when your version of Git is less than 2.28:

{% filename %}command-line{% endfilename %}

    $ git branch -M main
    

### Ignoring files

Git will track changes to all the files and folders in this directory, but there are some files we want it to ignore. We do this by creating a file called `.gitignore` in the base directory. Open up your editor and create a new file with the following contents:

{% filename %}.gitignore{% endfilename %}

    # Python
    *.pyc
    *~
    __pycache__
    
    # Env
    .env
    myvenv/
    venv/
    
    # Database
    db.sqlite3
    
    # Static folder at project root
    /static/
    
    # macOS
    ._*
    .DS_Store
    .fseventsd
    .Spotlight-V100
    
    # Windows
    Thumbs.db*
    ehthumbs*.db
    [Dd]esktop.ini
    $RECYCLE.BIN/
    
    # Visual Studio
    .vscode/
    .history/
    *.code-workspace
    

そして"djangogirls"フォルダーに`.gitignore`という名前で保存します。

> **備考：**ファイル名の先頭のドットは重要です! もしそのファイルを作るのが難しいなら、（Macをお使いの方はFinderからドット（ . ）で始まるファイルを作れません。）そういう時はエディタでSave Asから作成すれば問題ありません。 `.txt`や `.py`などの拡張子をファイル名に入れないように気をつけてください。 ファイル名が`.gitignore`でないとGitに認識されません。 LinuxとMacOSは、（`.gitignore` のように） `.<code>で始まる名前のファイルを隠しファイルとして扱います。通常の<code>ls`コマンドでは、これらのファイルは表示されません。 `.gitignore`fileを見つけるために、代わりに`ls -a`を使います。
> 
> **備考：** `.gitignore`ファイルで指定したファイルの1つが`db.sqlite3`です。 そのファイルはローカルデータベースで、すべてのユーザーと投稿が保存されます。 私達は標準的なウェブプログラミングの慣習に従います。つまり、ローカルのテストサイトとPythonAnywhere上の本番のウェブサイトでデータベースを分けるということです。 PythonAnywhereのデータベースは開発用のマシンと同じようにSQLiteにすることができますが、通常はMySQLというSQLiteよりもたくさんのサイト訪問者に対処できるデータベースを使用します。 どちらの方法でも、GitHubのコードのコピーではSQLiteデータベースを無視することで、これまでに作成したすべての投稿と管理者はそのままローカルで利用できますが、本番環境（ブログを公開するPythonAnywhereのことです）ではそれらを再び作成する必要があります。 ローカルデータベースは本当のブログ投稿をブログから削除してしまうことを心配せずに、さまざまなことをテストできるよい遊び場として考えるといいでしょう。

It's a good idea to use a `git status` command before `git add` or whenever you find yourself unsure of what has changed. This will help prevent any surprises from happening, such as wrong files being added or committed. The `git status` command returns information about any untracked/modified/staged files, the branch status, and much more. The output should be similar to the following:

{% filename %}command-line{% endfilename %}

    $ git status
    On branch main
    
    No commits yet
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
            .gitignore
            blog/
            manage.py
            mysite/
            requirements.txt
    
    nothing added to commit but untracked files present (use "git add" to track)
    

And finally we save our changes. Go to your console and run these commands:

{% filename %}command-line{% endfilename %}

    $ git add .
    $ git commit -m "My Django Girls app, first commit"
     [...]
     13 files changed, 200 insertions(+)
     create mode 100644 .gitignore
     [...]
     create mode 100644 mysite/wsgi.py
    

## GitHubにコードをプッシュする

Go to [GitHub.com](https://www.github.com) and sign up for a new, free user account. (If you already did that in the workshop prep, that is great!) Be sure to remember your password (add it to your password manager, if you use one).

Then, create a new repository, giving it the name "my-first-blog". Leave the "initialize with a README" checkbox unchecked, leave the .gitignore option blank (we've done that manually) and leave the License as None.

![](images/new_github_repo.png)

> **注** `my-first-blog`という名前は重要です。何か他のものを選択することもできますが、以下の手順では何度も繰り返す必要があります。他の名前を選択した場合は、 毎回それを置き換えてください。 できれば、`my-first-blog` の名前にしておきましょう。

On the next screen, you'll be shown your repo's clone URL, which you will use in some of the commands that follow:

![](images/github_get_repo_url_screenshot.png)

Now we need to hook up the Git repository on your computer to the one up on GitHub.

Type the following into your console (replace `<your-github-username>` with the username you entered when you created your GitHub account, but without the angle-brackets -- the URL should match the clone URL you just saw).

{% filename %}command-line{% endfilename %}

    $ git remote add origin https://github.com/<your-github-username>/my-first-blog.git
    $ git push -u origin main
    

When you push to GitHub, you'll be asked for your GitHub username and password (either right there in the command-line window or in a pop-up window), and after entering credentials you should see something like this:

{% filename %}command-line{% endfilename %}

    Counting objects: 6, done.
    Writing objects: 100% (6/6), 200 bytes | 0 bytes/s, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To https://github.com/ola/my-first-blog.git
    
     * [new branch]      main -> main
    Branch main set up to track remote branch main from origin.
    

<!--TODO: maybe do ssh keys installs in install party, and point ppl who dont have it to an extension -->

Your code is now on GitHub. Go and check it out! You'll find it's in fine company – [Django](https://github.com/django/django), the [Django Girls Tutorial](https://github.com/DjangoGirls/tutorial), and many other great open source software projects also host their code on GitHub. :)

{% include "/deploy/pythonanywhere.md" %}

# Check out your site!

The default page for your site should say "It worked!", just like it does on your local computer. Try adding `/admin/` to the end of the URL, and you'll be taken to the admin site. Log in with the username and password, and you'll see you can add new Posts on the server -- remember, the posts from your local test database were not sent to your live blog.

Once you have a few posts created, you can go back to your local setup (not PythonAnywhere). From here you should work on your local setup to make changes. This is a common workflow in web development – make changes locally, push those changes to GitHub, and pull your changes down to your live Web server. This allows you to work and experiment without breaking your live Web site. Pretty cool, huh?

Give yourself a *HUGE* pat on the back! Server deployments are one of the trickiest parts of web development and it often takes people several days before they get them working. But you've got your site live, on the real Internet!