.. image:: https://github.com/davidhalter/jedi-vim/blob/master/doc/logotype-a.svg

#################################################
jedi-vim - awesome Python autocompletion with VIM
#################################################

.. image:: https://travis-ci.org/davidhalter/jedi-vim.svg?branch=master
   :target: https://travis-ci.org/davidhalter/jedi-vim
   :alt: Travis-CI build status

jedi-vim is a VIM binding to the autocompletion library
`Jedi <http://github.com/davidhalter/jedi>`_.

Here are some pictures:

.. image:: https://github.com/davidhalter/jedi/raw/master/docs/_screenshots/screenshot_complete.png

Completion for almost anything (Ctrl+Space).

.. image:: https://github.com/davidhalter/jedi/raw/master/docs/_screenshots/screenshot_function.png

Display of function/class bodies, docstrings.

.. image:: https://github.com/davidhalter/jedi/raw/master/docs/_screenshots/screenshot_pydoc.png

Documentation (Pydoc) support (with highlighting, Shift+k).

There is also support for goto and renaming.


Get the latest from `github <http://github.com/davidhalter/jedi-vim>`_.

Documentation
=============

Documentation is available in your vim: ``:help jedi-vim``. You can also look
it up `on github <http://github.com/davidhalter/jedi-vim/blob/master/doc/jedi-vim.txt>`_.

You can read the Jedi library documentation `here <http://jedi.readthedocs.io/en/latest/>`_.

If you want to report issues, just use the github issue tracker. In case of
questions about the software, please use `stackoverflow
<https://stackoverflow.com/questions/tagged/jedi-vim>`_ and tag your question with ``jedi-vim``.


Contributing
============

We love Pull Requests! Read the instructions in ``CONTRIBUTING.md``.


Features
========

The Jedi library understands most of Python's core features. From decorators to
generators, there is broad support.

Apart from that, jedi-vim supports the following commands

- Completion ``<C-Space>``
- Goto assignment ``<leader>g`` (typical goto function)
- Goto definition ``<leader>d`` (follow identifier as far as possible,
  includes imports and statements)
- Goto (typing) stub ``<leader>s``
- Show Documentation/Pydoc ``K`` (shows a popup with assignments)
- Renaming ``<leader>r``
- Usages ``<leader>n`` (shows all the usages of a name)
- Open module, e.g. ``:Pyimport os`` (opens the ``os`` module)


Installation
============

Requirements
------------
You need a VIM version that was compiled with Python 2.7 or later
(``+python`` or ``+python3``).  You can check this from within VIM using
``:python3 import sys; print(sys.version)`` (use ``:python`` for Python 2).

Manual installation
-------------------

You might want to use `pathogen <https://github.com/tpope/vim-pathogen>`_ or
`Vundle <https://github.com/gmarik/vundle>`_ to install jedi-vim.

The first thing you need after that is an up-to-date version of Jedi. Install
``git submodule update --init --recursive`` in your jedi-vim repository.

Example installation command using Pathogen:

.. code-block:: sh

    git clone --recursive https://github.com/davidhalter/jedi-vim.git ~/.vim/bundle/jedi-vim

Example installation using Vundle:

Add the following line in your `~/.vimrc`
    
.. code-block:: vim

    Plugin 'davidhalter/jedi-vim'

For installing Jedi, ``pip install jedi`` will also work, but you might run
into issues when working in virtual environments. Please use git submodules.


Installation with your distribution
-----------------------------------

On Arch Linux, you can also install jedi-vim from official repositories as
`vim-jedi <https://www.archlinux.org/packages/community/any/vim-jedi/>`__.
It is also available on
`Debian (≥8) <https://packages.debian.org/vim-python-jedi>`__ and
`Ubuntu (≥14.04) <http://packages.ubuntu.com/vim-python-jedi>`__ as
vim-python-jedi.
On Fedora Linux, it is available as
`vim-jedi <https://apps.fedoraproject.org/packages/vim-jedi>`__.

Please note that this version might be quite old compared to using jedi-vim
from Git.

Caveats
-------

Note that the `python-mode <https://github.com/klen/python-mode>`_ VIM plugin seems
to conflict with jedi-vim, therefore you should disable it before enabling
jedi-vim.

To enjoy the full features of jedi-vim, you should have VIM >= 7.3, compiled with
``+conceal`` (which is not the case on some platforms, including OS X). If your VIM
does not meet these requirements, the parameter recommendation list may not appear
when you type an open bracket after a function name. Please read
`the documentation <http://github.com/davidhalter/jedi-vim/blob/master/doc/jedi-vim.txt>`_
for details.


Settings
========

Jedi is by default automatically initialized. If you don't want that I suggest
you disable the auto-initialization in your ``.vimrc``:

.. code-block:: vim

    let g:jedi#auto_initialization = 0

There are also some VIM options (like ``completeopt`` and key defaults) which
are automatically initialized, but you can skip this:

.. code-block:: vim

    let g:jedi#auto_vim_configuration = 0


You can make jedi-vim use tabs when going to a definition etc:

.. code-block:: vim

    let g:jedi#use_tabs_not_buffers = 1

If you are a person who likes to use VIM-splits, you might want to put this in your ``.vimrc``:

.. code-block:: vim

    let g:jedi#use_splits_not_buffers = "left"

This options could be "left", "right", "top", "bottom" or "winwidth". It will decide the direction where the split open.

Jedi automatically starts the completion, if you type a dot, e.g. ``str.``, if
you don't want this:

.. code-block:: vim

    let g:jedi#popup_on_dot = 0

Jedi selects the first line of the completion menu: for a better typing-flow
and usually saves one keypress.

.. code-block:: vim

    let g:jedi#popup_select_first = 0

Jedi displays function call signatures in insert mode in real-time, highlighting
the current argument. The call signatures can be displayed as a pop-up in the
buffer (set to 1 by default (with the conceal feature), 2 otherwise),
which has the advantage of being easier to refer to (but is a hack with
many drawbacks since it changes the buffer's contents),
or in Vim's command line aligned with the function call (set to 2), which
can improve the integrity of Vim's undo history.

.. code-block:: vim

    let g:jedi#show_call_signatures = "1"

Here are a few more defaults for actions, read the docs (``:help jedi-vim``) to
get more information. If you set them to ``""``, they are not assigned.

.. code-block:: vim

    NOTE: subject to change!

    let g:jedi#goto_command = "<leader>d"
    let g:jedi#goto_assignments_command = "<leader>g"
    let g:jedi#goto_stubs_command = "<leader>s"
    let g:jedi#goto_definitions_command = ""
    let g:jedi#documentation_command = "K"
    let g:jedi#usages_command = "<leader>n"
    let g:jedi#completions_command = "<C-Space>"
    let g:jedi#rename_command = "<leader>r"

A few examples of setting up your project:

.. code-block:: vim

    let g:jedi#environment_path = "<leader>d"

Finally, if you don't want completion, but all the other features, use:

.. code-block:: vim

    let g:jedi#completions_enabled = 0

FAQ
===

I don't want the docstring window to popup during completion
------------------------------------------------------------

This depends on the ``completeopt`` option. Jedi initializes it in its
``ftplugin``. Add the following line to your ``.vimrc`` to disable it:

.. code-block:: vim

    autocmd FileType python setlocal completeopt-=preview


I want <Tab> to do autocompletion
---------------------------------

Don't even think about changing the Jedi command to ``<Tab>``,
use `supertab <https://github.com/ervandew/supertab>`_!


The completion is too slow!
---------------------------

1. Completion of complex libraries (like Numpy) should only be slow the first
   time you complete them. After that the results should be cached and very fast.

2. If it is still slow after the initial completion and you have installed the
   python-mode Vim plugin, try disabling its rope mode:

   .. code-block:: vim

       let g:pymode_rope = 0

   See issue `#163 <https://github.com/davidhalter/jedi-vim/issues/163>`__.

3. You can also use `deoplete-jedi <https://github.com/zchee/deoplete-jedi>`__
   for completions, which uses Jedi, but does completions asynchronously
   (requires Neovim).
   It makes sense to use both jedi-vim and deoplete-jedi, but you should disable
   jedi-vim's completions then:

   .. code-block:: vim
   
       let g:jedi#completions_enabled = 0

Testing
=======

jedi-vim is being tested with a combination of `vspec
<https://github.com/kana/vim-vspec>`_ and `py.test <http://pytest.org/>`_.

The tests are in the ``test`` subdirectory, you can run them calling::

    py.test

The tests are automatically run with `travis
<https://travis-ci.org/davidhalter/jedi-vim>`_.
