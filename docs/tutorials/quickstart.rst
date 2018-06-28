.. _tutorial_quickstart:

Tutorial: JupyterHub in under 10 minutes
========================================

Goal
----

By the end of this tutorial, you should have a JupyterHub with some admin
users and user environment with packages you want installed. This is 80% of what
most users need, so is a great place to start

Pre-requisites
--------------

#. A fresh Ubuntu 18.04 server
#. Full root access
#. Some familiarity with the command line
#. Public IP for your server, so you can access your hub from the internet

Step 1: Install the Littlest JupyterHub (TLJH)
----------------------------------------------

``ssh`` into the server, and install TLJH.

.. code-block:: bash

   curl https://raw.githubusercontent.com/yuvipanda/the-littlest-jupyterhub/master/installer/install.bash | sudo bash -

This takes about 1-3 minutes to finish. When completed, you can visit the
public IP of your server to use your JupyterHub! You can log in with any username
and password combination.

Step 2: Add admin user
----------------------

You should add yourself as an admin user, so you can administer the JupyterHub
from inside JupyterHub itself. Making someone admin gives them ``root`` access to
the server, allowing them to make whatever changes they want.

TLJH is configured with a ``config.yaml`` files, written in `YAML <https://yaml.org>`_ syntax.
We will modify ``config.yaml`` to list admin users, and then restart JupyterHub to
let the changes take effect.

1. Open the ``config.yaml`` file for editing.

   .. code-block:: bash

      sudo nano /opt/tljh/config.yaml

2. Add usernames that should have admin access.

   .. code-block:: yaml

      users:
        admin:
          - user1
          - user2

   Be careful around the syntax - indentation matters, and you should be using
   spaces and not tabs.

   When you are done, save the file and exit. In ``nano``, you can do this with
   ``Ctrl+X`` key.

3. Restart jupyterhub so the changes can take effect.

   .. code-block:: bash

      sudo systemctl restart jupyterhub

   This should not disrupt any active users on your JupyterHub.

   If the user you made admin is already logged in, you might have to restart your
   notebook server via the Control Panel page accessed from top right of your web
   interface for your new superpowers to take effect.

4. Open a terminal in your notebook server (New -> Terminal) & check if sudo works.

   .. code-block:: console

     $ sudo -E id
       uid=0(root) gid=0(root) groups=0(root)

Congratulations, you are now an admin user in JupyterHub! Most administrative
actions can now be performed from inside the Terminal in Jupyter Notebooks,
without requiring SSH usage.

Step 3: Install conda / pip packages for all users
--------------------------------------------------

The **User Environment** is a conda environment that is shared by all users
in the JupyterHub. Libraries installed in this environment are immediately
available to all users. Admin users can install packages in this environment
with ``sudo -E``.

1. As an admin user, open a terminal in your notebook server
2. Install ``numpy`` from `conda-forge <https://conda-forge.org/>`_.

   .. code-block:: bash

      sudo -E conda install -c conda-forge numpy

   The ``sudo -E`` is very important!

3. Install ``there`` with ``pip``

   .. code-block:: bash

      sudo -E pip install there

The packages ``numpy`` and ``there`` are now available to all users in JupyterHub!