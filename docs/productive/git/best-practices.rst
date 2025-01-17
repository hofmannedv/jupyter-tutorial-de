Git Best Practices
==================

* Macht früh Commits!

  Macht euren ersten Commit nachdem ihr die initiale Installation
  fertiggestellt habt und noch bevor ihr erste Änderungen vornehmt. Für ein
  Cookiecutter-Template z.B. nach den folgenden Schritten:

  .. code-block:: console

    $ pipenv run cookiecutter https://github.com/veit/cookiecutter-namespace-template.git
    full_name [Veit Schiele]:
    email [veit@cusy.io]:
    github_username [veit]:
    project_name [cusy.example]:
    …

  Falls in eurem Projekt noch keine ``.gitignore``-Datei vorhanden ist, solltet
  ihr diese anlegen und zumindest ``.ipynb_checkpoints`` und
  ``*/.ipynb_checkpoints/*`` ausschließen:

  Falls ihr versehentlich schon entsprechende Dateien in euer Git-Repository
  eingecheckt habt, könnt ihr diese wieder entfernen mit:

  .. code-block:: console

    $ git rm -r .ipynb_checkpoints/

  Eine Übersicht über weitere ``.gitignore``-Einträge
  erhaltet ihr entweder im Repository `dotfiles
  <https://github.com/veit/dotfiles>`_ oder auf der Website `gitignore.io
  <https://gitignore.io/>`_.

  Anschließend können diese initialen Änderungen eingecheckt werden mit:

  .. code-block:: console

    $ cd cusy.example
    $ git init
    $ git add *
    $ git add .gitignore
    $ git commit -m 'Initial commit'
    $ git remote add origin ssh://git@github.com:veit/cusy.example.git
    $ git push -u origin main

  Auch eine ``README.rst``-Datei sollte in jedem Repository vorhanden sein, in
  der das Deployment und der grundsätzliche Aufbau des Codes beschrieben wird.

* Macht oft Commits!

  Dies erleichtert euch:

  * die Eingrenzung von Fehlern
  * das Verständnis für den Code
  * die zukünftige Wartung und Pflege.

  Falls ihr doch einmal mehrere Änderungen an einer Datei durchgeführt habt,
  könnt ihr diese auch später noch in mehrere Commits aufteilen mit:

  .. code-block:: console

    $ git add -p my-changed-file.py

* Ändert nicht die veröffentlichte Historie!

  Auch wenn ihr zu einem späteren Zeitpunkt herausfindet, dass ein Commit, der
  mit ``git push`` bereits veröffentlicht wurde, einen oder mehrere Fehler
  enthält, so solltet ihr dennoch niemals versuchen, diesen Commit ungeschehen zu
  machen. Vielmehr solltest Du durch weitere Commits den oder die aufgetretenen
  Fehler zu beheben.

* Wählt einen Git-Workflow!

  Wählt einen Workflow, der am besten zu eurem Projekt passt. Projekte sind
  keineswegs identisch und ein Workflow, der zu einem Projekt passt, muss
  nicht zwingend auch in einem anderen Projekt passen. Auch kann sich initial
  ein anderer Workflow empfehlen als im weiteren Fortschritt des Projekts.

* Macht sinnvolle Commits!

  Mit dem Erstellen aufschlussreicher und beschreibender Commit-Nachrichten
  erleichtert ihr die Arbeit im Team ungemein. Sie ermöglichen anderen, eure
  Änderungen zu verstehen. Auch sind sie zu einem späteren Zeitpunkt hilfreich
  um nachvollziehen zu können, welches Ziel mit dem Code erreicht werden
  sollte.

  Üblicherweise sollten kurze, 50–72 Zeichen lange Nachrichten angegeben
  werden, die in einer Zeile ausgegeben werden, z.B. mit
  ``git log --oneline``.

  Mit ``git blame`` könnt ihr euch auch später noch für jede Zeile angeben
  lassen, in welcher Revision und von welchem Autor sie kam. Weitere
  Informationen hierzu findet ihr in der Git-Dokumentation: `git-blame
  <https://git-scm.com/docs/git-blame>`_.

  Wenn ihr Gitmojis in euren Commit-Nachrichten verwendet, könnt ihr später
  leicht die Absicht des Commits erkennen.

  .. note::

    * `gitmoji.dev <https://gitmoji.dev/>`_
    * `github.com/carloscuesta/gitmoji
      <https://github.com/carloscuesta/gitmoji>`_
    * `github.com/carloscuesta/gitmoji-cli
      <https://github.com/carloscuesta/gitmoji-cli>`_
    * `Visual Studio Code Extension
      <https://marketplace.visualstudio.com/items?itemName=seatonjiang.gitmoji-vscode>`_

  GitLab interpretiert bestimmte Commit-Nachrichten auch als Links, z.B.:

  .. code-block:: console

    $ git commit -m "Awesome commit message (Fixes #21 and Closes group/otherproject#22)"

  * zu Issues: ``#123``

    * auch in anderen Projekten: ``othergroup/otherproject#123``

  * zu Merge Requests: ``!123``
  * zu Snippets: ``$123``

  Dabei sollte es zu jedem Commit mindestens ein Ticket geben, das
  ausführlichere Hinweise zu den Änderungen geben sollte.

  .. note::
    * `A Note About Git Commit Messages
      <https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html>`_

* Wartet euer Repository regelmäßig!

  Folgende Wartungsarbeiten solltet ihr regelmäßig durchführen:

  * Validiert das Repo mit ``git fsck``.
  * Komprimiert das Repo mit ``git gc`` bzw. ``git gc --aggressive``.

    .. seealso::
        * `git gc <https://git-scm.com/docs/git-gc>`_
        * `Git Interna - Wartung und Datenwiederherstellung
          <https://git-scm.com/book/de/v2/Git-Interna-Wartung-und-Datenwiederherstellung>`_

  * Bereinigt die Remote Tracking Branches mit ``git remote update --prune``.
  * Überprüft vergessene Arbeiten mit ``git stash list``.

* Überprüft eure Repositories regelmäßig auf unerwünschte Dateien!

  Mit `Gitleaks <https://github.com/zricethezav/gitleaks>`_ könnt ihr eure
  Repositories regelmäßig auf ungewollt gespeicherte Zugangsdaten überprüfen.

  Ihr könnt Gitleaks auch automatisch als GitLab-Action ausführen. Hierzu müsst
  ihr die `Secret-Detection.gitlab-ci.yml
  <https://gitlab.com/gitlab-org/gitlab/-/blob/master/lib/gitlab/ci/templates/Jobs/Secret-Detection.gitlab-ci.yml>`_-Vorlage
  :abbr:`z.B. (zum Beispiel)` in eine Stufe namens ``secrets-detection`` in
  eurer ``.gitlab-ci.yml``-Datei einbinden:

  .. code-block:: yaml

     stages:
       - secrets-detection

     gitleaks:
       stage: secrets-detection
       include:
         - template: Security/Secret-Detection.gitlab-ci.yml

  Die Vorlage erstellt *Secret Detection*-Aufträge in eurer CI/CD-Pipeline und
  durchsucht den Quellcode eures Projekts nach *Secrets*. Die Ergebnisse werden
  als `Secret Detection Report Artefakt
  <https://docs.gitlab.com/ee/ci/yaml/artifacts_reports.html#artifactsreportssecret_detection>`_
  gespeichert, den ihr später herunterladen und analysieren könnt.

  .. seealso::

     * `GitLab Secret Detection
       <https://docs.gitlab.com/ee/user/application_security/secret_detection/>`_

  Mit `git-filter-repo <https://github.com/newren/git-filter-repo>`_ könnt ihr
  unerwünschte Dateien, seien es Zugangsdaten oder große Binärdateien aus eurer
  Git-Historie entfernen.

  Alternativ könnt ihr auch auf der Kommandozeile die Daten löschen.

  * Löschen des letzten Commits

    .. code-block:: console

        $ git reset HEAD^ --hard
        $ git push origin -f

  * Löschen anderer Commits

    .. code-block:: console

        $ git rebase -i SHA origin/main

    ``-i``
        interaktiver Modus, in dem euer Standardeditor geöffnet wird und eine
        Liste aller Commits nach dem zu entfernenden Commit mit dem Hash-Wert
        :samp:`{SHA}` angezeigt wird, z.B.:

        .. code-block:: console

            pick d82199e Update readme
            pick 410266e Change import for the interface
            …

        Wenn ihr nun eine Zeile entfernt, so wird dieser Commit nach dem
        Speichern und Schließen des Editors gelöscht. Anschließend kann das
        entfernte Repository aktualisiert werden mit:

        .. code-block:: console

            $ git push origin HEAD:main -f

  * Ändern einer Commit-Nachricht

    Dies lässt sich ebenfalls einfach mit ``rebase`` realisieren wobei ihr in
    eurem Editor nicht die Zeile löschen sondern in der Zeile ``pick`` durch
    ``r`` (*reword*) ersetzen müsst.

  * Entfernen einer Datei aus der Historie

    Eine Datei kann vollständig aus Git-Historie des aktuellen Branches entfernt
    werden mit:

    .. code-block:: console

        $ git filter-repo --invert-paths --path path/somefile
        $ git push --no-verify --mirror

    .. note::
       Informiert die Team-Mitglieder, dass sie erneut einen Klon des Repository
       erstellen sollten.

  * Entfernen einer Zeichenkette aus der Historie

    .. code-block:: console

        $ git filter-repo --message-callback 'return re.sub(b"^git-svn-id:.*\n", b"", message, flags=re.MULTILINE)'

  .. seealso::
    * `git-filter-repo — Man Page <https://www.mankier.com/1/git-filter-repo>`_
    * `git-reflog <https://git-scm.com/docs/git-reflog>`_
    * `git-gc <https://git-scm.com/docs/git-gc>`_
