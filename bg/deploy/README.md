# Внедряване!

> **Забележка** Следващата глава понякога може да бъде малко трудна за преминаване. Продължи и я завърши; внедряването е важна част от процеса на разработване на уебсайтове. Тази глава е поставена в средата на ръководството, така че твоят ментор да ти помогне с малко по-сложния процес на вдигане на уебсайта ти онлайн. Това означава, че все още можеш да завършиш ръководството самостоятелно, ако ти липсва време.

Досега твоят уебсайт беше достъпен само на твоя компютър. Сега ще научите как да го прехвърлите в онлайн пространството! Разгръщането е процесът на публикуване на приложението ви в Интернет, така че хората най-накрая да могат да отидат и да видят приложението ви. :)

Както научихте, уебсайт трябва да бъде разположен на сървър. В интернет има много доставчици на сървъри, ще използваме [PythonAnywhere](https://www.pythonanywhere.com/). PythonAnywhere е безплатен за малки приложения, които нямат твърде много посетители, така че определено засега ще ви бъде достатъчно.

Другата външна услуга, която ще използваме е [GitHub](https://www.github.com), която е услуга за хостинг на код. Има и други, но почти всички програмисти имат GitHub акаунт в наши дни, а сега и вие!

Тези три места ще бъдат важни за вас. Вашият локален компютър ще бъде мястото, където правите разработка и тестване. Когато сте доволни от промените, ще поставите копие на програмата си в GitHub. Вашият уебсайт ще бъде на PythonAnywhere и ще го актуализирате, като получите ново копие на вашия код от GitHub.

# Git

> **Note** If you already did the [installation steps](../installation/README.md), there's no need to do this again – you can skip to the next section and start creating your Git repository.

{% include "/deploy/install_git.md" %}

## Стартираме нашето Git хранилище

Git проследява промените в определен набор от файлове в т.нар. склад (или за кратко "репо"). Нека започнем еднo за нашия проект. Отворете конзолата и стартирайте тези команди в директорията `djangogirls`:

> **Забележка** Проверете текущата си работна директория с команда `pwd` (Mac OS X / Linux) или `cd` (Windows), преди да инициализирате хранилището. Трябва да сте в папката `djangogirls`.

{% filename %}command-line{% endfilename %}

    $ git init
    Initialized empty Git repository in ~/djangogirls/.git/
    $ git config --global user.name "Your Name"
    $ git config --global user.email you@example.com
    

Инициализирането на git хранилището е нещо, което трябва да направим само веднъж за всеки проект (и няма да се налага да въвеждате отново потребителското име и имейла).

### Adjusting your branch name

If the version of Git that you are using is older than **2.28**, you will need to change the name of your branch to "main". To determine the version of Git, please enter the following command:

{% filename %}command-line{% endfilename %}

    $ git --version
    git version 2.xx...
    

Only if the second number of the version, shown as "xx" above, is less than 28, will you need to enter the following command to rename your branch. If it is 28 or higher, please continue to "Ignoring files". As in "Initializing", this is something we need to do only once per project, as well as only when your version of Git is less than 2.28:

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
    

And save it as `.gitignore` in the "djangogirls" folder.

> **Забележка** Точката в началото на името на файла е важна! Ако имате проблеми с създаването му (Macs не харесва да създавате файлове, които започват с точка чрез Finder, например), след това използвайте функцията "Save As" в редактора си; това е бронеустойчиво. И не забравяйте да добавите `.txt`, `.py` или друго разширение към името на файла - той ще бъде разпознат от Git само ако името е просто `.gitignore`. Linux и MacOS взимат файловете с име, което започва с `.` (като `.gitignore`) за скрити и нормалната команда `ls` няма да показва тези файлове. Вместо това използвайте `ls -a`, за да видите файла `.gitignore`.
> 
> **Забележка** Един от файловете, които сте посочили във вашия `.gitignore` файл е `db.sqlite3`. Този файл е вашата локална база данни, където се съхраняват всички ваши потребители и публикации. Ще следваме стандартната практика за уеб програмиране, което означава, че ще използваме отделни бази данни за вашия локален тестващ сайт и вашия уеб сайт на живо в PythonAnywhere. Базата данни на PythonAnywhere може да бъде SQLite, като вашата разработваща машина, но обикновено ще използвате такава, наречена MySQL, която може да се справи с много повече посетители на сайта, отколкото SQLite. Така или иначе, като игнорирате вашата SQLite база данни за копието на GitHub, това означава, че всички публикувани досега публикации и superuser ще бъдат достъпни само локално и ще трябва да създавате нови в производството. Трябва да мислите за вашата локална база данни като за добра площадка, където можете да тествате различни неща и да не се страхувате, че ще изтриете истинските си публикации от блога.

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
    

## Избутване на кода ви към GitHub

Go to [GitHub.com](https://www.github.com) and sign up for a new, free user account. (If you already did that in the workshop prep, that is great!) Be sure to remember your password (add it to your password manager, if you use one).

Then, create a new repository, giving it the name "my-first-blog". Leave the "initialize with a README" checkbox unchecked, leave the .gitignore option blank (we've done that manually) and leave the License as None.

![](images/new_github_repo.png)

> **Забележка** Името `my-first-blog` е важно - бихте могли да изберете нещо друго, но това ще се случва много пъти в инструкциите по-долу и ще трябва да го замествате всеки път. Вероятно е по-лесно да се придържаме към името `my-first-blog`.

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