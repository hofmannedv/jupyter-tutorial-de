Pipenv und Spack
================

Pipenv wurde bereits zur :doc:`Installation von Jupyter Notebooks
</first-steps/install>` verwendet. Wir benötigen hier jedoch Pipenv für unsere
:doc:`Spack Environments <../../envs/spack/envs>` um
einerseits binärkompatible Builds mit Spack erzeugen zu können und andererseits
Python-Pakete für die Datenerhebung, -Visualisierung etc. einfach nutzen zu
können.

Aktiviert hierfür zunächst die passende Python-Version aus dem
Spack-Environment:

   .. code-block:: console

    $  spack env activate python-38
    $ spack env status
    ==> In environment python-38
    $ which python
    /srv/jupyter/spack/var/spack/environments/python-38/.spack-env/view/bin/python

Das bestehende Pipenv-Environment könnt ihr anschließend installieren mit:

   .. code-block:: console

    $ cd ~/jupyter-tutorial/pipenvs/python-374/
    $ pipenv --python=/Users/veit/jupyter-tutorial/spackenvs/python-374/.spack-env/view/bin/python --site-packages
    $ pipenv install
    Creating a virtualenv for this project…
    Pipfile: /Users/veit/jupyter-tutorial/pipenvs/python-374/Pipfile
    Using /Users/veit/jupyter-tutorial/spackenvs/python-374/.spack-env/view/bin/python3.7 (3.7.4) to create virtualenv…
    …

Dies verwendet das mit Spack installierte Environment und installiert weitere
Pakete.

.. seealso::

    * `Pipenv and Other Python Distributions
      <https://pipenv.pypa.io/en/latest/advanced/#pipenv-and-other-python-distributions>`_
