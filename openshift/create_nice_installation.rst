Create a Nice Installation
==========================

A template is used to create a new installation. It can be found in the `Ansible Git Repository`_.

.. _Ansible Git Repository: https://git.tocco.ch/gitweb?p=ansible.git


Step by Step Instructions
-------------------------

#. Clone the `Ansible Git Repository`_

   .. code::

       git clone ssh://USER@git.tocco.ch:29418/ansible.git

#. Go to the ``openshift`` directory within the repository.

   .. code::

       cd ansible/openshift

#. Create all resources required

   .. code::

       oc process -f nice-template.yml -v CUSTOMER=${CUSTOMER} -v … | oc create -f -

   Parameter are specified using ``-v KEY=VALUE``, this is the list of **mandatory** parameters:

   =================== ===============================================================================================
    Key                 Value
   =================== ===============================================================================================
    CUSTOMER            Name of the customer (e.g. agogis or ecap but never :strike:`agogistest` or
                        :strike:`ecaptest`).

    INSTALLATION        Name of the installation (e.g. ecap or ecaptest)

                        :subscript:`The name of a test system MUST end in "test"!`

    RUN_ENV             Run environment which must be one of ``production`` or ``test``.
   =================== ===============================================================================================

   Additionally, these optional parameters are available. **(Default values should suffice mostly.)**

   ===================== ==========================================================================================
    Key                   Value
   ===================== ==========================================================================================
    FLUENTD_TARGET        URL to the :term:`Fluentd` logging service.

                          :subscript:`Leave blank to log to /app/var/log/nice.log instead.`

    JAVA_MEM              Max. memory available to Java (e.g. ``1.5g`` or ``512m``).

    DB_PASSWORD           Password for database access.

                          :subscript:`Randomly generated if left off.`

    DB_SERVER             URL to the Postgres database server.

    DOCKER_REGISTRY_URL   URL to the Docker image registry.

    NGINX_IMAGE_NAME      Name of the :term:`Nginx` Docker image.

    SOLR_DISK_SPACE       Persistent disk space available to :term:`Solr` (e.g. ``512m`` or ``5g``).

    SOLR_IMAGE_URL        Name of the Solr Docker image.
   ===================== ==========================================================================================

.. important::

    The installation needs also to be :ref:`created in Teamcity <create-installation-in-teamcity>`.

.. note::

  The installation is automatically started once :term:`CD` pushes an image to the Docker registry.
