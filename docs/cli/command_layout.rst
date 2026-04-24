Command Structure and Arguments
===============================

``cwms-cli`` uses commands, subcommands, and options. The position of each
part matters.

General pattern
---------------

Most commands follow this shape:

.. code-block:: text

   cwms-cli [global options] command [command options] [subcommand] [subcommand options]

Read it from left to right:

- ``cwms-cli`` starts the program
- global options apply to the whole CLI
- a command selects the feature area, such as ``users`` or ``blob``
- a subcommand drills down further when needed, such as ``roles add``
- options belong to the command level where they appear

Global options come first
-------------------------

Global options must be placed right after ``cwms-cli`` because they apply to
the whole program.

Examples:

.. code-block:: bash

   cwms-cli --log-file ./cwms-cli.log --log-level DEBUG users roles
   cwms-cli -q blob list
   cwms-cli --help

These are global options:

- ``--log-file``
- ``--no-color``
- ``--log-level``
- ``-q`` / ``--quiet``
- ``-h`` / ``--help``
- ``-V`` / ``--version``

Commands do not use a leading dash
----------------------------------

Commands such as ``users``, ``blob``, and ``load`` are command names, not
options. Write them without ``-`` or ``--``.

Use this:

.. code-block:: bash

   cwms-cli users roles
   cwms-cli blob list
   cwms-cli load --help

Do not use this:

.. code-block:: bash

   cwms-cli -users
   cwms-cli -blob
   cwms-cli -load

Why this matters
----------------

In CLI tools:

- names with ``-`` or ``--`` are options
- names without dashes are commands or arguments

So ``users`` is a command group, while ``--office`` is an option.

Examples by level
-----------------

Top-level command:

.. code-block:: bash

   cwms-cli users

Nested command:

.. code-block:: bash

   cwms-cli users roles add

Option attached to the nested command:

.. code-block:: bash

   cwms-cli users roles add --user-name q0hectest --roles "Viewer Users"

Global options still go near the front:

.. code-block:: bash

   cwms-cli --log-level DEBUG users roles add --user-name q0hectest --roles "Viewer Users"

Another nested example:

.. code-block:: bash

   cwms-cli load timeseries ids-all --source-office SWT --target-cda http://localhost:8081/cwms-data/

Common mistakes
---------------

Mistake:

.. code-block:: bash

   cwms-cli -users

Use instead:

.. code-block:: bash

   cwms-cli users

Mistake:

.. code-block:: bash

   cwms-users

Use instead:

.. code-block:: bash

   cwms-cli users

Mistake:

.. code-block:: bash

   cwms-cli users --log-level DEBUG roles

Use instead:

.. code-block:: bash

   cwms-cli --log-level DEBUG users roles

How to tell where an option belongs
-----------------------------------

Use help at the level you are working on:

.. code-block:: bash

   cwms-cli --help
   cwms-cli users --help
   cwms-cli users roles --help
   cwms-cli load timeseries ids-all --help

Each help screen shows only the options available at that level.

See also
--------

- :doc:`Installation and Setup <setup>`
- :doc:`CLI reference <../cli>`
- :doc:`Users commands <users>`
