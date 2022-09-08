Git е "система за контрол на версиите", използвана от много програмисти. Този софтуер може да проследява промените във файловете с течение на времето, така че да можете да заредите конкретни версии по-късно. Нещо като функцията „проследяване на промените“ в програми за текстообработка (например, Microsoft Word или LibreOffice Writer), но много по-мощна.

## Инсталиране на Git

<!--sec data-title="Installing Git: Windows" data-id="git_install_windows"
data-collapse=true ces-->

Можете да свалите Git от [git-scm.com](https://git-scm.com/). Можеш да натиснеш „next“ на всички стъпки, с изключение на две: в стъпката, където се изисква да избереш твоя редактор, трябва да избереш Nano, и в стъпката, озаглавена „Настройка на вашата PATH среда“, избери "Използване на Git и незадължителни Unix инструменти от командния ред на Windows" (най-долната опция). Освен това, настройките по подразбиране са добре. Разгледайте Windows стил, Unix стил за окончанията на редовете е добре.

During installation, if you are presented with the option of "Adjusting the name of the initial branch in new repositories", please choose to "Override the default" and use "main". This will align your installation of Git with the broad direction of the global developer community, and the "main" branch will be used through the remainder of this tutorial. Please see https://sfconservancy.org/news/2020/jun/23/gitbranchname/ and https://github.com/github/renaming for further discussion of this subject.

Do not forget to restart the command prompt or PowerShell after the installation finished successfully. <!--endsec-->

<!--sec data-title="Installing Git: OS X" data-id="git_install_OSX"
data-collapse=true ces-->

Download Git from [git-scm.com](https://git-scm.com/) and follow the instructions.

During installation, if you are presented with the option of "Adjusting the name of the initial branch in new repositories", please choose to "Override the default" and use "main". This will align your installation of Git with the broad direction of the global developer community, and the "main" branch will be used through the remainder of this tutorial. Please see https://sfconservancy.org/news/2020/jun/23/gitbranchname/ and https://github.com/github/renaming for further discussion of this subject.

> **Забележка** Ако използвате OS X 10.6, 10.7 или 10.8, ще трябва да инсталирате версията на git от тук: [Инсталатор на Git за OS X Snow Leopard](https://sourceforge.net/projects/git-osx-installer/files/git-2.3.5-intel-universal-snow-leopard.dmg/download)

<!--endsec-->

<!--sec data-title="Installing Git: Debian or Ubuntu" data-id="git_install_debian_ubuntu"
data-collapse=true ces-->

{% filename %}command-line{% endfilename %}

```bash
$ sudo apt install git
```

### Adjusting your default branch name

This will align your installation of Git with the broad direction of the global developer community, and the "main" branch will be used through the remainder of this tutorial. Please see https://sfconservancy.org/news/2020/jun/23/gitbranchname/ and https://github.com/github/renaming for further discussion of this subject.

{% filename %}command-line{% endfilename %}

    $ git config --global --add init.defaultBranch main
    

<!--endsec-->

<!--sec data-title="Installing Git: Fedora" data-id="git_install_fedora"
data-collapse=true ces-->

{% filename %}command-line{% endfilename %}

```bash
$ sudo dnf install git
```

### Adjusting your default branch name

This will align your installation of Git with the broad direction of the global developer community, and the "main" branch will be used through the remainder of this tutorial. Please see https://sfconservancy.org/news/2020/jun/23/gitbranchname/ and https://github.com/github/renaming for further discussion of this subject.

{% filename %}command-line{% endfilename %}

    $ git config --global --add init.defaultBranch main
    

<!--endsec-->

<!--sec data-title="Installing Git: openSUSE" data-id="git_install_openSUSE"
data-collapse=true ces-->

{% filename %}command-line{% endfilename %}

```bash
$ sudo zypper install git
```

### Adjusting your default branch name

This will align your installation of Git with the broad direction of the global developer community, and the "main" branch will be used through the remainder of this tutorial. Please see https://sfconservancy.org/news/2020/jun/23/gitbranchname/ and https://github.com/github/renaming for further discussion of this subject.

{% filename %}command-line{% endfilename %}

    $ git config --global --add init.defaultBranch main
    

<!--endsec-->