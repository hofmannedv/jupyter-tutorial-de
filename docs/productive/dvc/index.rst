Daten verwalten mit ``DVC``
===========================

Für Datenanalysen und vor allem bei Machine Learning ist es äußerst wertvoll,
verschiedene Versionen von Analysen, die mit verschiedenen Datensätzen und
Parametern durchgeführt wurden, reproduzieren zu können. Um jedoch
reproduzierbare Analysen zu erhalten, müssen sowohl die Daten als auch das
Modell (einschließlich der Algorithmen, Parameter. etc.) versioniert werden.
Die Versionierung von Daten für reproduzierbare Analysen ist aufgrund der
Datengröße ein größeres Problem als die Versionierung von Modellen. Werkzeuge
wie `DVC <https://dvc.org/>`_ helfen bei der Verwaltung von Daten, indem Nutzer
diese mit einem :doc:`Git <../git/index>`-artigen Workflow an einen entfernten
Datenspeicher übertragen können. Hierdurch vereinfacht sich der Abruf bestimmter
Versionen von Daten um eine Analyse zu reproduzieren.

DVC wurde entwickelt, um ML-Modelle und Datensätze gemeinsam nutzen zu können
und nachvollziehbar zu verwalten. Es arbeitet zwar mit verschiedenen
Versionsverwaltungen zusammen, benötigt diese jedoch nicht. Im Gegensatz z.B. zu
`DataLad <https://www.datalad.org/>`_/`git-annex
<https://git-annex.branchable.com/>`_ ist es auch nicht auf Git als
Versionsverwaltung beschränkt, sondern kann z.B auch zusammen mit Mercurial
verwendet werden, siehe `github.com/crobarcro/dvc/dvc/scm.py
<https://github.com/crobarcro/dvc/blob/master/dvc/scm.py>`_. Zudem nutzt es
ein eigenes System zum Speichern der Dateien mit Unterstützung u.a. für SSH und
HDFS.

DataLad konzentriert sich hingegen mehr auf die Entdeckung und Verwendung von
Datasets, die dann einfach mit Git verwaltet werden. DVC hingegen speichert
jeden Schritt der Pipeline in einer separaten ``.dvc``-Datei, die dann durch
Git verwaltet werden kann.

Diese ``.dvc``-Dateien erlauben jedoch praktische Tools zur Manipulation und
Visualisierung von DAGs, siehe z.B. die :doc:`Visualisierung der DAGs
<pipeline>`.

Schließlich lassen sich mit :ref:`dvc remote <dvc-remote>` auch externe 
Abhängigkeiten angeben.

.. seealso::
   * `Tutorial <https://dvc.org/doc/tutorial>`_
   * `Documentation <https://dvc.org/doc>`_
   * `Git Repository <https://github.com/iterative/dvc>`_

Installation
------------

DVC lässt sich mit Pipenv installieren. Beachtet dabei jedoch bitte, dass ihr
hierbei die Extras explizit angeben müsst. Dies können ``[ssh]``, ``[s3]``,
``[gs]``, ``[azure]``, und ``[oss]`` oder ``[all]`` sein. Für ``ssh`` sieht das
Kommando dann so aus:

.. code-block:: console

    $ pipenv install dvc[ssh]

Alternativ kann DVC auch über andere Paketmanager installiert werden:

.. tab:: Debian/Ubuntu

   .. code-block:: console

      $ sudo wget https://dvc.org/deb/dvc.list -O /etc/apt/sources.list.d/dvc.list
      $ sudo apt update
      $ sudo apt install dvc

.. tab:: macOS

   .. code-block:: console

      $ brew install iterative/homebrew-dvc/dvc

.. note::

   Bitte beachtet, dass das folgende Beispiel mit einer aktuellen DVC-Version
   erstellt wurde (1.0.0a9), die :abbr:`z.T. (zum Teil)` eine andere Syntax als
   frühere Versionen verwendet. Dies könnt ihr aktuell (8. Juni 2020) nur mit
   pip installieren:

   .. code-block:: console

      $ pipenv install dvc[all]==1.0.0a9

.. toctree::
    :hidden:

    init
    pipeline
    params
    metrics
    dag
    reproduce
    integration
    fds
