.. _notebook_interfaces:

Notebook Interfaces (Classic, JupyterLab, nteract)
==================================================

By default, logging into TLJH puts you in the classic Jupyter Notebook interface
we all know and love. However, there are at least two other popular notebook
interfaces you can use:

1. `JupyterLab <http://jupyterlab.readthedocs.io/en/stable/>`_
2. `nteract <https://nteract.io/>`_

Both these interfaces are also shipped with TLJH by default. You can try them
temporarily, or set them to be the default interface whenever you login.

Trying alternate interface tempoarily
-------------------------------------

When you log in & start your server, by default the URL in your browser
will be something like ``/user/<username>/tree``. The ``/tree`` is what tells
the notebook server to give you the classic notebook interface.

If you change ``/tree`` to ``/lab``, you will get the JupyterLab interface.

If you change ``/tree`` to ``/nteract``, you will get he nteract interface.

You can play around with them and see what fits your use cases best.

Changing default notebook interface
-----------------------------------

You can change the default interface users get when they log in by modifying
``config.yaml`` as an admin user.

#. Open the ``config.yaml`` file.

   .. code-block:: bash

      sudo nano /opt/tljh/config.yaml

#. To launch **JupyterLab** when users log in, add the following snippet to the config

   .. code-block:: yaml

      userEnvironment:
        defaultApp: jupyterlab

#. Alternatively, to launch **nteract** when users log in, add the following snippet to the config

   .. code-block:: yaml

      userEnvironment:
        defaultApp: nteract

#. Save and exit the editor. With ``nano``, you can do this by pressing ``Ctrl-X``.

#. Apply the changes by restarting JupyterHub. This should not disrupt current users.

   .. code-block:: yaml

      sudo systemctl restart jupyterhub

   If this causes problems, check the :ref:`troubleshoot_logs_jupyterhub` for clues
   on what went wrong.

Users might have to restart their servers from control panel to get the new interface.
