Getting Started
================

Introduction
++++++++++++

A couple of installs and using the ReadTheDocs command line interface to create your documentation project will have you up and editing real documentation in a matter of minutes.  We will set up a few requirements and generating a documentation project that we can edit and run locally.

Install ReadTheDocs prerequisites
+++++++++++++++++++++++++++++++++

We will:

	- install all the prerequisites:
		#. *Python*; 
		#. *Sphinx*; 
		#. the *ReadTheDocs.io* theme.
	- use command line interface to create the project; 
	- build the project; 
	- make a "*Hello World!*" type change; 

First, we note the main ReadTheDocs sites (home page here https://readthedocs.org/).  Somewhere on the home page will link to a *getting started* guide (https://docs.readthedocs.io/en/latest/getting_started.html).  Feel free to browse around here for materials not covered in this *Document*.  We will be back here later.

*Python*
--------

#. We download the latest version of *Python* (https://www.*python*.org/downloads/).  Download the ``.exe`` installer and run it; 
#. check the option to ``Add Python X.X to PATH``, then ``Install Now``.  This might take a minute; 
#. ``Close`` the window.  (We have the option to ``Disable path length limit``, but we won't mess around with it now).

Now that *Python* has been installed, we can install the other prerequisites.  Open ``cmd``.  We need to use the *Python* ``pip`` command to run these: ::

	pip install sphinx
	pip install sphinx_rtd_theme

At this point we have installed both *sphinx* and the *ReadTheDocs.io* theme, and are all set to create our doc project.

Creating a documentation project
++++++++++++++++++++++++++++++++

We will:
	#. build a sample documentation site; 
	#. use the ``sphinx-quickstart`` command; 
	#. consider whether to put the project inside a code project folder or on its own; 
	#. consider the *project name* and *author name(s)*; 

For our example, we will put our doc project in a place of its own and give it a name.  Open a normal instance of ``cmd``: ::

	mkdir docproject
	cd docproject
	sphinx-quickstart

In most of the cases the defaults are fine and the text promptig you for a decision is pretty helpful. ::

	> Root path for the documentation [.]:

We can leave this alone by hitting ``Enter``.  This is where to put the docs and we will use the current directory ``docproject``. ::

	> Separate source and build directories (y/n) [n]:

We can leave the source and build directory config alone as well, which means that source content will be placed directly in the root folder and the build will go in a folder within root directory. ::

	> Name prefix for templates and static dir [_]:

Prefixing directories for static content with an underscore is fine, so we will leave this too.  ::

	> Project name:

Next up comes our name prompts and we will provide out choice for these.  I will use: ::

	> Project name: Doc Project
	> Author name(s): Hertz Zhang

	> Project release []:

Moving one, we are asked about versions.  If we are documenting a specific software project, we may want to provide these; *else* leave them blank (hit ``Enter``). ::

	> Project language [en]:

Next up comes a language option.  This *Document* will be in English. ::

	> Source file suffix [.rst]:

Then a suffix for source files; leave the ``.rst`` as the default for *reStructuredText*. ::

	> Name your master document (without suffix) [index]:

We can leave the starting doc named ``index.rst``. ::

	> Do you eant to use the epub builder (y/n) [n]:

We can opt into ``.epub`` support if we want to produce something can could be read on an ebook reader. Press *either* ``y`` *or* ``n``. ::

	> autodoc: automatically insert docstrings from modules (y/n) [n]:

	> doctest: automatically test code snippets in doctest blocks (y/n) [n]:
	> intersphinx: link between Sphinx documentation of different projects (y/n) [n]:
	> todo: write "todo" entries that can be shown or hidden on build (y/n) [n]:
	> coverage: checks for documentation coverage (y/n) [n]:
	> imgmath: include math, rendered as PNG or SVG images (y/n) [n]:
	> mathjax: include math, rendered in the browser by MathJax (y/n) [n]:
	> ifconfig: conditional inclusion of content based on config values (y/n) [n]:
	> viewcode: include links to the source code of documented Python objects (y/n) [n]:
	> githubpages: create .nojekyll file to publish the document on GitHub pages (y/n) [n]:

Next up comes the option to include some *sphinx* extensions in our projects.  We won't use any of them--many, if not all are related to documenting *Python* projects. ::

	> Create Makefile? (y/n) [y]:
	> Create windows command file (y/n) [y]:

We agree to create a ``Makefile`` and a ``command```file to simplify our build process, *then* we're done.

.. Note::

	Our ``.cmd`` should look something like this: ::

		Creating file .\conf.py.
		Creating file .\index.rst.
		Creating file .\Makefile.
		Creating file .\make.bat.

		Finished: An initial directory structure has been created.

		You should now populate your master file .\index.rst and create other documentation
		source files. Use the Makefile to build the docs, like so:
		   make builder
		where "builder" is one of the supported builders, e.g. html, latex or linkcheck.

If we do a ``dir`` in the current directory, we should see ::

	07/08/2018  16:45    <DIR>          .
	07/08/2018  16:45    <DIR>          ..
	07/08/2018  16:45             5,408 conf.py
	07/08/2018  16:45               469 index.rst
	07/08/2018  16:45               814 make.bat
	07/08/2018  16:45               607 Makefile
	07/08/2018  16:45    <DIR>          _build
	07/08/2018  16:45    <DIR>          _static
	07/08/2018  16:45    <DIR>          _templates
	               4 File(s)          7,298 bytes

which are the files and folder that have been created.

.. Note::

	To build the project, we run::

		make html

	**NB** ::

		The HTML pages are in _build\html.

	which means that the HTML pages are saved in the ``_build\html`` directory under your project directory.

.. Note::

	To run the ``index.html`` file that's in the ``_build\html`` directory: ::

		_build\html\index.html

	and the webpage will open in your chosen web browser.  **NB** the theme on the bottom of the webpage is *Alabaster*, which we will change later.

*Visual Studio Code*
++++++++++++++++++++

To edit our doc project we need two things:  a *text editor* and a *terminal*.  Personally I use *Sublime* for text editing for its functionality.  In this document, we will also explore Visual Studio Code ("*vsc*").

.. Note::
	
	I recommend the following packages if we're using *Sublime* (whilst in sublime): ::

		Ctrl + Shift + P
		Package Control: Install Package
		RestructuredText Improved

		Ctrl + Shift + P
		Package Control: Install Package
		sublime-rst-completion

	These packages improves ``.rst`` syntax colour highlighting and auto-completion.  We may need to restart your *Sublime* app for them to take effect.  When editing a *.rst* file, we should set the syntax to ``reStructuredText improved`` where necessary: ::

		Alt + V
		S
		reStructuredText improved

We will also download *vsc* (https://code.visualstudio.com/).  Download the ``.exe`` installer, and run it.  It's a free, lightweight code editor that runs on any platform and has lots of great plugins, plus an integrated terminal where we can do our build.  It also knows about projects and folders and has get source control management functionality built in.  Open *vsc*.

We can drag the ``docproject`` folder into the *vsc* window to open the project.  Since we haven't opened any files, the ``Welcome`` page stages visible; we can close it.

On the left navigation pane, we can see the project structure:

- The ``_build`` folder contains the result of our ``make`` command, and if we expand the ``html`` folder under ``_build``, we can see some of the ``.html`` files and some of the various resources and other content that the ``make`` process created.
- Our ``_static`` and ``_templates`` folders are empty initially.  We will get back to them later.
- The ``index.rst`` file is the simple starter page for our doc project, and we will be looking at the *reStructuredText* markup language in more detail later.
- The ``conf.py`` is a configuration file written in *Python* that tells the ``make`` process many of the options about our project, and we will modify this to get the *ReadTheDocs.io* theme applied.
- Lastly, the ``Makefile`` and ``make.bat`` just support the build process and are not all that interesting (``make.bat`` is a batch file that supports the ``make`` command in your terminal).

Apply the *ReadTheDocs.io* theme
++++++++++++++++++++++++++++++++

To apply the *ReadTheDocs.io* theme, open the ``conf.py`` file and head down to the line ::

	html_theme = 'alabaster'

and change it to ::

	html_theme = 'sphinx_rtd_theme'

Save ``conf.py`` and open the integrated powershell terminal in *vsc* (``Ctrl + '`` (*apostrophe*)), then run: ::

	./make html

and if we run ::

	./_build\html\index.html

then we can see that the *ReadTheDocs.io* theme has been applied.
