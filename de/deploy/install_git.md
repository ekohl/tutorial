Git ist ein "Versionsverwaltungssystem" für Dateien und Code, das von vielen Programmierern benutzt wird. Diese Software kann Änderungen an Dateien über die Zeit verfolgen, so dass du bestimmte Versionen im Nachhinein wieder aufrufen kannst. Sie hat Ähnlichkeit mit der Funktion "Änderungen nachverfolgen" in Textverarbeitungsprogrammen (z. B. Microsoft Word oder LibreOffice Writer), ist jedoch weitaus leistungsfähiger.

## Git installieren

<!--sec data-title="Installing Git: Windows" data-id="git_install_windows"
data-collapse=true ces-->

Du kannst Git von [git-scm.com](https://git-scm.com/) herunterladen. Du kannst bei allen Schritten außer zweien "next" klicken: Wähle im Schritt, in dem du einen Editor aussuchen sollst, "Nano"; und bei der Anweisung "Adjusting your PATH environment", wähle die Einstellung "Run Git and associated Unix tools from the Windows command-line" (die letzte Option). Die anderen Voreinstellungen sind ok. "Checkout"-Stil "Windows" und "Commit" mit "Unix line endings" (Zeilenende im Unix-Format) sind die richtigen Einstellungen.

Wenn dir während der Installation die Option "Adjusting the name of the initial branch in new repositories" angezeigt wird, wähle "Override the default" aus und nutze "main" als initialen Branch. This will align your installation of Git with the broad direction of the global developer community, and the "main" branch will be used through the remainder of this tutorial. Please see https://sfconservancy.org/news/2020/jun/23/gitbranchname/ and https://github.com/github/renaming for further discussion of this subject.

Vergiss nicht, die Kommandozeile zu schließen und wieder zu öffnen, nachdem du die Installation erfolgreich durchgeführt wurde.<!--endsec-->

<!--sec data-title="Installing Git: OS X" data-id="git_install_OSX"
data-collapse=true ces-->

Lade Git von [git-scm.com](https://git-scm.com/) herunter und folge dann den Anweisungen.

During installation, if you are presented with the option of "Adjusting the name of the initial branch in new repositories", please choose to "Override the default" and use "main". This will align your installation of Git with the broad direction of the global developer community, and the "main" branch will be used through the remainder of this tutorial. Please see https://sfconservancy.org/news/2020/jun/23/gitbranchname/ and https://github.com/github/renaming for further discussion of this subject.

> **Hinweis:** Falls du OS X 10.6, 10.7, oder 10.8 verwendest, muss du die Git-Version unter folgendem Link installieren: [Git installer for OS X Snow Leopard](https://sourceforge.net/projects/git-osx-installer/files/git-2.3.5-intel-universal-snow-leopard.dmg/download)

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