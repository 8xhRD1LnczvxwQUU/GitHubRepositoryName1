..	Automating Workflow
	===
		Introduction
		+++
		Git and GitHub
		Create and load GitHub repository for the source code
		Set up ReadTheDocs hosting
		Continuous integration / continuous delivery
		Setting up CI/CD on ReadTheDocs
		Pull Requests
		Configure GitHub to require Pull requests to Master
		Submit a Change via a Pull request
		Approve and Merge the Pull request
		Summary

Automating Workflow
===================



Introduction
++++++++++++

So far we have learnt how to create a doc project and also to create content.  In this *Document*, we will set up ReadTheDocs hosting for our project, along with the typical Git workflow to control and simplify the way that updates get made to the docs.  We will cover the following:

#. Git and GitHub; 
	#. introduction; 
	#. prerequisites; 
	#. establishing a repository with our code; 
#. ReadTheDocs; 
	#. setting up an account; 
	#. hook to GitHub and our doc repo; 
#. Require Pull requests; 
#. doing a Pull request.

Git and GitHub
++++++++++++++

**Git** is a distributed version control system.  Other source control systems include *subversion*, *cvs*, and *team foundation version control* ("*tfvc*").  There are a lot of compelling reasons to use Git over some of the other options, such as the way it stores files, the ease for uses of switching branches, and the prevalence of its use throughout the open source world.  

The `website <https://git-scm.com/>`_ also has some good general info about Git and the command line options available.  We will need this installed for what we are doing and we will go over just what we specifically need for this *Document*.

A key term we will see or hear with respect to Git is a **repository** (or *repo*).  This refers to a single code "project" (in the looser sense of the word).  A repository might be defined as having the collection of solution and project files or directories that constitute a logical application or package, including any applicable tests or other such stuff.  We will be creating a single repository for our doc project, but if it makes sense to do so, our doc project could be a part of a larger repository.

**GitHub** is a website that hosts Git repositories and implements the Git interface points.  There are many other platforms that can host Git repositories, e.g. *GitLab*, *Bitbucket*, the *Team Foundation Server* since 2015, and *vsts* in the cloud.  For our initial demo, we will be working with GitHub, but we will explore the same functionality in *vsts* and on-premises *tfs*.

In this document, we will cover just what we need from Git which will set us up and running.

.. Attention::	

	**Try Git**

	https://try.github.io/ is an interactive Try Git kit that lets us explore some of the command line functionality of Git right in the Browser in a little tutorial.

.. Note:: 

	**Local Git installation**

	To use Git functionality on your local machine, we can download it here: https://git-scm.com/.  Download and run the ``.exe`` installer.  An install-wizard should appear:

	#. ``Information``.  The first step is a license note agreement; read through it and click ``Next >``; 
	#. ``Select Destination Location``.  We confirm the directory in which Git will be installed; we can use the default; 
	#. ``Select Components``.  Now we have some options to choose from; we can use the defaults; 
	#. ``Set Start Menu Folder``.  This will create a Git shortcut in the *Start Menu* folder; leave as default; 
	#. ``Adjust your PATH environment``.  Then we can choose how to modify the Git PATH environment variable; the default is fine for this exercise; 
	#. ``Choosing HTTPS transport backend``.  Leave the default ``Use the OpenSSL library`` selected.  
	#. ``Configure the line ending conversions``.  Git can perform some line ending conversions; leave as default; 
	#. ``Configure the terminal emulator to use with Git Bash``.  Leave as default; 
	#. ``Configure extra options``.  Leave as default; 
	#. Click ``Install``.
	
	When this completes, the Git Source commands will be available on our local machine.

.. Note::

	**Create a GitHub account**
	
	*If* we can sign into GitHub (https://github.com/) and have the option to create a ``New repository``, *then* we are good to go; *else* create a GitHub account and log in.



Create and load GitHub repository for the source code
+++++++++++++++++++++++++++++++++++++++++++++++++++++

We will:

#. take the local directory we have been working on our machine and turn it into a Git repository on GitHub; 
#. add a ``.gitignore`` config file to our local folder to make the repository ignore our ``_build`` directory for source control purposes; 
#.  turn our local directory into a local Git repository by using a Git initialise command; 
#.  configure the local repo to be remotely connected to the GitHub repository we set up in Step 1; 
#.  do an initial push from the local folder into the remote repository, which will push all our source files up into GitHub; 

These steps are all one-time set-up steps, and the regular workflow for making changes and getting them committed will be a little different and a little easier.

We start the process to get our doc code into a GitHub repository.

.. Note::

	**Create a** ``New repository`` **on GitHub**

	#. Log into our GitHub account; 
	#. Click on the (green) ``New repository`` button; 
	#. Give the Repository a name; 
	#. Click ``Create repository``.

.. Attention::

	**Quick setup**

	Grab the ``HTTPS`` URL for the repository and save it somewhere.  We will use it later.  It looks something like: ::

		https://github.com/UserNameHere/RepoNameHere.git

.. https://github.com/8xhRD1LnczvxwQUU/GitHubRepositoryName1.git

Open *vsc*.

.. Note::

	**Create a** ``.gitignore`` **file**

	#. in *vsc*, under the ``docproject`` directory, add a file called ``.gitignore`` (hover over the ``docproject`` tab and click the ``New File`` icon); 
	#. open ``.gitignore`` and add ::
		
		_build

	as the first and only line to the file; 

	We need to add a ``.gitignore`` file so our ``_build`` folder contents, which amounts to quite a few files, will not be part of what lives in our Git repository.  This is a special file that Git will look at as it monitors the repository we will create.  The ``_build`` line makes sure that Git doesn't look at that directory for change monitoring and source control.  

Now we can initialise the Git repository for this directory.  We can do this from the command line, but we will use the *vsc* ``Source Control`` tab (``Ctrl + Shift + G``).  We see a note that ``There are no active source control providers``.  

Set up ReadTheDocs hosting
++++++++++++++++++++++++++



Continuous integration / continuous delivery
++++++++++++++++++++++++++++++++++++++++++++



Setting up CI/CD on ReadTheDocs
+++++++++++++++++++++++++++++++



Pull Requests
+++++++++++++



Configure GitHub to require Pull requests to Master
+++++++++++++++++++++++++++++++++++++++++++++++++++



Submit a Change via a Pull request
++++++++++++++++++++++++++++++++++



Approve and Merge the Pull request
++++++++++++++++++++++++++++++++++



Summary
+++++++




.. toctree::
   :maxdepth: 2
   :caption: Contents:

.. \end{toctree}

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
