``isort``
=========

`isort <https://github.com/timothycrosley/isort>`_ formatiert eure
``import``-Anweisungen in getrennte und sortierte Blöcke.

Installation
------------

.. code-block:: console

    $ pipenv install isort

Konfiguration
-------------

``isort`` lässt sich z.B. in der ``pyproject.toml``-Datei konfigurieren:

.. code-block:: ini

    [tool.isort]
    atomic=true
    force_grid_wrap=0
    include_trailing_comma=true
    lines_after_imports=2
    lines_between_types=1
    multi_line_output=3
    not_skip="__init__.py"
    use_parentheses=true

    known_first_party="jupyter-tutorial"
    known_third_party=["mpi4py", "numpy", "requests"]

Um Pakete von Drittanbietern gegenüber euren Projektimporten zu erkennen, könnt
ihr euer Projekt zusammen mit ``isort`` installieren.

.. note::
    Mit isort 5 könnt ihr Profile verwenden. Dies erleichtert die Konfiguration
    von isort, um auch zukünftig mit :doc:`black` zusammenzuspielen:

    .. code-block:: ini

        isort --profile black .
