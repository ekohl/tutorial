Chromebookを使わない場合は、このセクションを飛ばして、[Pythonのインストール](http://tutorial.djangogirls.org/en/installation/#install-python) に進んでください。 もし利用している場合は、普通のインストールの作業とは少し異なります。 インストール手順の残りの部分は無視できます。

### クラウドIDE (PaizaCloud Cloud IDE, AWS Cloud9, Glitch.com)

クラウドIDEはコードエディタと、インターネットにつながって動作し、ソフトウェアをインストールしたり、書いたり、実行したりできるコンピュータへのアクセスを提供するツールです。 チュートリアルを通して、クラウドIDEはまるであなたの*ローカルマシン*のように動作するでしょう。 みんながOS XやUbuntuやWindowsでやるのと同じようにターミナルからコマンドを実行できますが、そのターミナルはクラウドIDEが準備したどこかのコンピュータに接続されています。 さて、いろいろなクラウドIDE（PaizaCloud Cloud IDE, AWS Cloud9, Glitch.com）について見ていきましょう。 クラウドIDEのうちどれかを選んで、指示に従ってください。

#### PaizaCloud Cloud IDE

1. [PaizaCloud Cloud IDE](https://paiza.cloud/) へ移動します。
2. アカウントを登録します。
3. *新規サーバ作成* をクリックして、Djangoを選択してください。
4. （ウィンドウの左側にある）「ターミナル」をクリックします。

左側にサイドバーといくつかボタンのある画面が見えていると思います。 「ターミナル」ボタンをクリックして、下記のようなプロンプトが表示されたターミナルウィンドウを開いてください：

{% filename %}Terminal{% endfilename %}

    $
    

これでPaizaCloud Cloud IDEのターミナルは準備できました。 ウィンドウを大きくしたいときは、サイズを変えたり最大化したりできますよ。

#### AWS Cloud9

現在、Cloud 9 はAWSのアカウント作成とクレジットカード情報の登録が必須になっています。

1. [Chrome ウェブストア](https://chrome.google.com/webstore/detail/cloud9/nbdmccoknlfggadpfkmcpnamfnbkmkcp)から、Cloud 9 をインストールしてください。
2. [c9.io](https://c9.io)に行って、*AWS Cloud9をはじめる* をクリックしてください。
3. AWSアカウントを作成してください。（クレジットカード情報の登録が必要ですが、このチュートリアルは無料利用枠で進めることができます。）
4. AWSのダッシュボードを開き、検索ボックスで *Cloud9* と入力し選択してください。
5. Cloud9のダッシュボードで、*Create environment (環境の作成)* を選択します。
6. 名前は *django-girls* としておきましょう。
7. ”Configure settings (設定の構成)”のステップでは、”Environment Type (環境タイプ)”に *Create a new instance for environment (EC2) (新しいインスタンスを作成する (EC2))* を、”Instance type (インスタンスタイプ)”に *t2.micro* を選択します（"Free-tier eligible (無料利用枠で利用できる)" と書かれているはずです）。 ”Cost-saving setting (コスト削減の設定)”はデフォルトの選択のままにします。その他の設定もデフォルトにしておきましょう。
8. *Next step (次のステップ)* を選択します。
9. *Create environment (環境の作成)* を選択します。

サイドバー、文章が書かれた大きなメインウィンドウ、そして下部にはこのような小さなウィンドウが表示されています：

{% filename %}bash{% endfilename %}

    yourusername:~/workspace $
    

この下の部分が、あなたのターミナルです。このターミナルから、遠くにあるCloud 9のコンピュータに指示を送ることができます。ウィンドウのサイズを変更して少し大きくすることもできます。

#### Glitch.com Cloud IDE

1. Glitch.com<0>に行く</li> 
    
    - アカウントをサインアップ(https://glitch.com/signup)するか、GitHubアカウントを持っている場合はそれを使用します。(以下のGitHubの手順を参照してください)
    - *新規プロジェクト* をクリックし、 *hello-webpage* を選択します。
    - ツールドロップダウンリスト(ウィンドウの左下にある)をクリックします。 次に、ターミナルのボタンを以下のようなプロンプトとともにターミナルを開くために、ターミナルボタンをクリックします。</ol> 
    
    {% filename %}Terminal{% endfilename %}
    
        app@name-of-your-glitch-project:~
        
    
    クラウドIDEとしてGlitch.comを使用する場合、仮想環境を作成する必要はありません。 代わりに、以下のファイルを手動で作成してください。
    
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
    
    これらのファイルが作成されたら、ターミナルに行き、次のコマンドを実行して最初のDjangoプロジェクトを作成します。
    
    {% filename %}Terminal{% endfilename %}
    
        django-admin.py startproject mysite .
        refresh
        
    
    詳細なエラーメッセージを表示するには、GlitchアプリケーションのDjangoデバッグログを有効にします。 `mysite/settings.py` ファイルの末尾に以下を追加するだけです。
    
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
    
    これにより、Djangoの操作や出てくる可能性のあるエラーメッセージを詳細に記述した `debug.log` ファイルが作成されるので、ウェブサイトが動作しない場合の修正がとても簡単になります。
    
    Glitch プロジェクトの最初の再起動は失敗するはずです。 （一番上のドロップダウンボタン `Show` をクリックし、`In a New Window` をクリックした場合、`DisallowedHost` のエラーメッセージが表示されます）。 この段階では心配しないでください。`mysite/settings.py` ファイルでプロジェクトのDjango設定を更新すれば、チュートリアルですぐに修正されます。 
    
    ### 仮想環境
    
    仮想環境 (virtualenvとも呼ばれます) は、取り組んでいるプロジェクト用に、便利なコードを詰め込んでおけるプライベートボックスのようなものです。 様々なプロジェクトの様々なコードがプロジェクト間で混ざってしまわないように、仮想環境を使います。
    
    Run:
    
    {% filename %}Cloud 9{% endfilename %}
    
        mkdir djangogirls
        cd djangogirls
        python3 -m venv myvenv
        source myvenv/bin/activate
        pip install django~={{ book.django_version }}
        
    
    (note that on the last line we use a tilde followed by an equal sign: `~=`).
    
    ### GitHub
    
    [GitHub](https://github.com) アカウントを作成します。
    
    ### PythonAnywhere
    
    Django Girlsチュートリアルの目次には、デプロイと呼ばれるものに関するチャプターがあります。これはあなたの新しいWebアプリケーションの原動力となるコードを取得して、それを公にアクセス可能なコンピューター（サーバーと呼ばれます）に移動するプロセスです。これにより、あなたのやったことを他の人が見ることができるようになります。
    
    Chromebookでチュートリアルを行うとき、この部分は少し奇妙に感じるかもしれません。 すでにインターネットに接続されているコンピュータを使用しているからです。 (例えば、ノートパソコンだとか) しかし、Cloud 9のワークスペースを「開発中」の場所、PythonAnywhere をより完成したものを披露する場所として考えると分かりやすいです。
    
    したがって、新しいPythonAnywhereアカウントにサインアップしてください。 [ www.pythonanywhere.com ](https://www.pythonanywhere.com)