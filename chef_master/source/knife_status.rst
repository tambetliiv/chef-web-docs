=====================================================
knife status
=====================================================
`[edit on GitHub] <https://github.com/chef/chef-web-docs/blob/master/chef_master/source/knife_status.rst>`__

.. tag knife_status_summary

Use the ``knife status`` subcommand to display a brief summary of the nodes on a Chef Infra Server, including the time of the most recent successful Chef Infra Client run.

.. end_tag

Syntax
=====================================================
This subcommand has the following syntax:

.. code-block:: bash

   $ knife status (options)

Options
=====================================================
.. note:: .. tag knife_common_see_common_options_link

          Review the list of `common options </knife_options.html>`__ available to this (and all) knife subcommands and plugins.

          .. end_tag

This subcommand has the following options:

``QUERY``
   The search query used to identify a list of items on a Chef Infra Server. This option uses the same syntax as the ``search`` subcommand.

``--hide-by-mins``
   Hide nodes that have performed a successful Chef Infra Client run within the last specified number of minutes. The number of minutes to hide is provided as an integer, such as ``--hide-by-mins 10``. 

``-H``, ``--hide-healthy``
   Hide nodes on which a Chef Infra Client run has occurred within the previous hour.

   Deprecated in favor of the ``--hide-by-mins`` option in Chef Client 12.6 and above.
   
``-l``, ``--long``
   Display all attributes in the output and show the output as JSON.

``-m``, ``--medium``
   Display normal attributes in the output and to show the output as JSON.

``-r RUN_LIST``, ``--run-list RUN_LIST``
   A comma-separated list of roles and/or recipes to be applied.

.. note:: .. tag knife_common_see_all_config_options

          See `config.rb </config_rb_optional_settings.html>`__ for more information about how to add certain knife options as settings in the config.rb file.

          .. end_tag

Examples
=====================================================
The following examples show how to use this knife subcommand:

**View status, include run-lists**

.. tag knife_status_include_run_lists

To include run-lists in the status, enter:

.. code-block:: bash

   $ knife status --run-list

to return something like:

.. code-block:: bash

   20 hours ago, dev-vm.chisamore.com, ubuntu 10.04, dev-vm.chisamore.com, 10.66.44.126, role[lb].
   3 hours ago, i-225f954f, ubuntu 10.04, ec2-67-202-63-102.compute-1.amazonaws.com, 67.202.63.102, role[web].
   3 hours ago, i-a45298c9, ubuntu 10.04, ec2-174-129-127-206.compute-1.amazonaws.com, 174.129.127.206, role[web].
   3 hours ago, i-5272a43f, ubuntu 10.04, ec2-184-73-9-250.compute-1.amazonaws.com, 184.73.9.250, role[web].
   3 hours ago, i-226ca64f, ubuntu 10.04, ec2-75-101-240-230.compute-1.amazonaws.com, 75.101.240.230, role[web].
   3 hours ago, i-f65c969b, ubuntu 10.04, ec2-184-73-60-141.compute-1.amazonaws.com, 184.73.60.141, role[web].

.. end_tag

**View status using a time range**

To show the status of nodes on which the Chef Infra Client did not run successfully within the past hour, enter:

.. code-block:: bash 

   $ knife status --hide-by-mins 60

to return something like:

.. code-block:: bash 

   422492 hours ago, runner-1-432.lxc, centos 6.8.
   27 hours ago, union-3-432.lxc, centos 7.3.1611.

On systems running Chef Client 12.5 or prior:

.. code-block:: bash

   $ knife status --hide-healthy

to return something like:

.. code-block:: bash

   1 hour ago, i-256f884f, ubuntu 12.04, ec2-67-202-63-102.compute-1.amazonaws.com, 67.202.63.102, role[web].
   1 hour ago, i-a47823c9, ubuntu 10.04, ec2-174-129-127-206.compute-1.amazonaws.com, 184.129.143.111, role[lb].

**View status using a query**

.. tag knife_status_returned_by_query

To show the status of a subset of nodes that are returned by a specific query, enter:

.. code-block:: bash

   $ knife status "role:web" --run-list

to return something like:

.. code-block:: bash

   3 hours ago, i-225f954f, ubuntu 10.04, ec2-67-202-63-102.compute-1.amazonaws.com, 67.202.63.102, role[web].
   3 hours ago, i-a45298c9, ubuntu 10.04, ec2-174-129-127-206.compute-1.amazonaws.com, 174.129.127.206, role[web].
   3 hours ago, i-5272a43f, ubuntu 10.04, ec2-184-73-9-250.compute-1.amazonaws.com, 184.73.9.250, role[web].
   3 hours ago, i-226ca64f, ubuntu 10.04, ec2-75-101-240-230.compute-1.amazonaws.com, 75.101.240.230, role[web].
   3 hours ago, i-f65c969b, ubuntu 10.04, ec2-184-73-60-141.compute-1.amazonaws.com, 184.73.60.141, role[web].

.. end_tag

**View status for all nodes**

To view the status of all nodes in the organization, enter:

.. code-block:: bash

   $ knife status

to return something like:

.. code-block:: bash

   20 hours ago, dev-vm.chisamore.com, ubuntu 10.04, dev-vm.chisamore.com, 10.66.44.126
   3 hours ago, i-225f954f, ubuntu 10.04, ec2-67-202-63-102.compute-1.amazonaws.com, 67.202.63.102
   3 hours ago, i-a45298c9, ubuntu 10.04, ec2-174-129-127-206.compute-1.amazonaws.com, 174.129.127.206
   3 hours ago, i-5272a43f, ubuntu 10.04, ec2-184-73-9-250.compute-1.amazonaws.com, 184.73.9.250
   3 hours ago, i-226ca64f, ubuntu 10.04, ec2-75-101-240-230.compute-1.amazonaws.com, 75.101.240.230
   3 hours ago, i-f65c969b, ubuntu 10.04, ec2-184-73-60-141.compute-1.amazonaws.com, 184.73.60.141
