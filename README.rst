==============================================================
 The Simple Emacs Interface to `Ack <http://beyondgrep.com>`_-like Tools
==============================================================

This package integrates `ack <http://beyondgrep.com>`_ with `Emacs
<http://www.gnu.org/software/emacs>`_.  The resulting ``*ack*`` buffer
is just like vanilla ``*grep*`` but results come from your tool of
choice.

Not only ack, but Ack-like tools such as `the silver searcher (ag)
<https://github.com/ggreer/the_silver_searcher>`_, `ripgrep (rg)
<https://github.com/BurntSushi/ripgrep>`_ are well supported, as are
``git grep`` and ``hg grep``.

The program guesses good defaults -- including searching for the thing
at point -- but lets you input ``C-u`` to customize the directory,
commands, switches etc...

Install
-------

The current version can only be installed manually. Clone this repository

``$ git clone https://github.com/marianpiatkowski/ack-el.git``

and add ``ack-el`` to your ``load-path``:

.. code-block:: lisp

  (add-to-list 'load-path "path/to/ack-el")
  (require 'ack)
  (require 'pcmpl-ack)

Usage
-----

Just ``M-x ack`` or do something like ``(global-set-key (kbd "C-c
C-g") 'ack)``.

Since version 1.10 the default behavior for ``M-x ack`` has changed.
To set it to pre v1.10, put the following to your ``.emacs`` file:

``(setq ack-defaults-function 'ack-legacy-defaults)``

A quick search for the pattern at the current location can be done with ``M-x quick-ack``.

You may want to set the path to the ack executable explicitly, like on Windows for instance.

``(setq ack-command "C:/Wherever/I/Installed/Ack/Ack.exe")``

Screenshots
-----------

* ack

.. figure:: http://i.imgur.com/VwWyzAe.png
   :target: http://i.imgur.com/VwWyzAe.png
   :alt: ack.png

* git grep

.. figure:: http://i.imgur.com/rwjC4pa.png
   :target: http://i.imgur.com/rwjC4pa.png
   :alt: ack-git-grep.png

More Usage
----------

- Type ``M-x ack`` and provide a pattern to search.
- Type ``C-u M-x ack`` to search from current project root.
- Type ``C-u C-u M-x ack`` to interactively choose a directory to search.
- Type ``M-x quick-ack`` and search for the pattern under cursor.
- Type ``C-u M-x quick-ack`` to search for the pattern under cursor from current project root.
- Type ``C-u C-u M-x quick-ack`` to interactively choose a directory and search for the pattern
  under cursor.

While reading ack command and args from the minibuffer, the following
key bindings may be useful:

- ``M-I`` => insert a template for case-insensitive file name search
- ``M-G`` => insert a template for ``git grep``, ``hg grep`` or ``bzr grep``
- ``M-P`` => insert a template with ``--no-pager`` option
- ``M-Y`` => grab the symbol at point from the window before entering
  the minibuffer
- ``TAB`` => completion for ack options

If you use the above keybindings very often, stick the corresponding
command names in ``ack-minibuffer-setup-hook``. The following snippet
makes ``M-x ack`` insert a ``git|hg|bzr grep`` template if searching
from a project root. Then it will try to insert the symbol at point.

.. code-block:: lisp

  (add-hook 'ack-minibuffer-setup-hook 'ack-skel-vc-grep t)
  (add-hook 'ack-minibuffer-setup-hook 'ack-yank-symbol-at-point t)

Emacs23
-------

Check out the `emacs23
<https://github.com/leoliu/ack-el/tree/emacs23>`_ branch.

Bugs
----

https://github.com/marianpiatkowski/ack-el/issues

Contributors
------------
Phillip Lord. The original author and previous mantainer is Leo Liu.
