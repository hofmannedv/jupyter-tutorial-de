Produkt erstellen
=================

    »Nicht reproduzierbare Einzelereignisse sind für die Wissenschaft ohne
    Bedeutung.«[#]_

.. [#] Karl Popper in *Logik der Forschung*, 1935

Damit auch andere euren Code nutzen können, sollte er einige Bedingungen
erfüllen:

* Ihr solltet Euch nicht stillschweigend auf bestimmte Ressourcen und Umgebungen
  verlassen
* Erforderliche Software-Pakete und Hardware sollten in den Anforderungen
  angegeben werden
* Pfadangaben werden in einem anderen Kontext nur innerhalb eures Pakets oder in
  vorher generierten Verzeichnissen und Dateien funktionieren
* Teilt keine Geheimnisse wie Zugangsdaten oder interne IP-Nummern in eurem
  veröffentlichten Produkt

Es gibt diverse Werkzeuge, die Euch beim Erstellen von gemeinsam nutzbaren
Produkten unterstützen. Dies können Werkzeuge einerseits für die Versionierung
des :doc:`Quellcodes <git/index>` und der :doc:`Trainingsdaten <dvc/index>`
sowie für die Reproduzierbarkeit der :doc:`Ausführungsumgebungen <envs/index>`,
andererseits für das :doc:`testing`, :doc:`logging/index`, :doc:`Dokumentieren
<documenting>` und :doc:`Erstellen von Paketen <python-basics:libs/index>` sein.

.. seealso::

   * `Dustin Boswell, Trevor Foucher: The Art of Readable Code
     <https://learning.oreilly.com/library/view/~/9781449318482/>`_
   * TIB workshop «FAIR Data and Software»

     * `GitHub Page
       <https://tibhannover.github.io/2018-07-09-FAIR-Data-and-Software/>`_
     * `GitHub Repository
       <https://github.com/TIBHannover/2018-07-09-FAIR-Data-and-Software>`_
     * `Slides <https://doi.org/10.5281/zenodo.3707745>`_
   * `Dryad: Best practices for creating reusable data publications
     <https://datadryad.org/stash/best_practices>`_

.. toctree::
    :hidden:
    :titlesonly:
    :maxdepth: 0

    git/index
    dvc/index
    envs/index
    packaging
    documenting
    licensing
    cite/index
    testing
    logging/index
    qa/index
