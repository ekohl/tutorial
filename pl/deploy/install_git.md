Git jest "systemem kontroli wersji", którego używa wielu programistów. Program ten śledzi zmiany w plikach na przestrzeni czasu, dzięki czemu możesz później przywracać wybrane wersje tych plików. Trochę jak funkcja "Śledź zmiany" w programach do edytowania tekstu (np. programu Microsoft Word lub LibreOffice Writer), ale jest o wiele potężniejsza.

## Instalacja Gita

<!--sec data-title="Installing Git: Windows" data-id="git_install_windows"
data-collapse=true ces-->

Możesz ściągnąć Gita z [git-scm.com](https://git-scm.com/). Naciśnij "next" na wszystkich krokach z wyjątkiem dwóch: w kroku, w którym prosi o wybranie edytora, powinnaś wybrać Nano, a w kroku zatytułowanym "Adjusting your PATH environment" wybrać "Use Git and optional Unix tools from the Windows Command Prompt" (dolna opcja). Poza tym domyślne ustawienia są w porządku. Upewnij się jeszcze, że w kroku "Configuring the line ending conversions" wybrana jest opcja "Checkout Windows-style, commit Unix-style line endings".

During installation, if you are presented with the option of "Adjusting the name of the initial branch in new repositories", please choose to "Override the default" and use "main". This will align your installation of Git with the broad direction of the global developer community, and the "main" branch will be used through the remainder of this tutorial. Please see https://sfconservancy.org/news/2020/jun/23/gitbranchname/ and https://github.com/github/renaming for further discussion of this subject.

Do not forget to restart the command prompt or PowerShell after the installation finished successfully. <!--endsec-->

<!--sec data-title="Installing Git: OS X" data-id="git_install_OSX"
data-collapse=true ces-->

Download Git from [git-scm.com](https://git-scm.com/) and follow the instructions.

During installation, if you are presented with the option of "Adjusting the name of the initial branch in new repositories", please choose to "Override the default" and use "main". This will align your installation of Git with the broad direction of the global developer community, and the "main" branch will be used through the remainder of this tutorial. Please see https://sfconservancy.org/news/2020/jun/23/gitbranchname/ and https://github.com/github/renaming for further discussion of this subject.

> **Uwaga**Jeżeli działasz na OS X 10.6, 10.7 lub 10.8, będziesz musiała zainstalować wersję gita dostępną tutaj: [Git installer for OS X Snow Leopard](https://sourceforge.net/projects/git-osx-installer/files/git-2.3.5-intel-universal-snow-leopard.dmg/download)

<!--endsec-->

<!--sec data-title="Installing Git: Debian or Ubuntu" data-id="git_install_debian_ubuntu"
data-collapse=true ces-->

{% filename %}command-line{% endfilename %}

```bash
sudo apt install git
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