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

Automating workflow
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

.. Note::

	**Initialise Git repository**

	#. click on the ``Git`` icon to ``Initialize Repository``; an ``Explorer`` window will pop up; 
	#. click the ``Initialize Repository`` button; 
	#. type in a ``Commit Message`` for the new repository (e.g. *initial commit*), then ``Commit`` (``Ctrl + Enter``); 
	#. we may see a note about: ::

		There are no staged changes to commit.

		Would you like to automatically stage all your changes and commit them directly?

	click ``Yes``.

	We've initialised a new repository in Git.  Since this is brand new, all the existing files are "initial changes" needing to be committed to the repository, hence the ``initial commit``.

	Staging changes is beyond the scope of this *Document*, but we might think of it like creating shelf sets in *tfvc*.  

Having completed the initialisation and the first commit, we now have a local Git repository and the current state of all our source code is now at a known point.  All of this is so far still on our local machine.  Now we need to connect to a remote repository and do a push.

The integrated menu options and Git functionality do not currently support the two operations we need to do, so we will open the *vsc* terminal for this (``Ctrl + '`` (apostrophe)).  We start by adding a remote origin link to the URL that GitHub gave us.  

.. Note::

	**Remote GitHub repository and Push**

	#. open a *vsc* terminal (``Ctrl + '`` (apostrophe)); ::
	   
		git remote add origin GitHubRepoURLHere
		git push -u origin master

	#. open your GitHub Repository URL (or *refresh* the page); 
	#. we see that our code has been uploaded to our GitHub repository.

	We just push-ed with the ``-u`` flag to the ``master`` branch.  Some objects will be reviewed and written onto GitHub.

Set up ReadTheDocs hosting
++++++++++++++++++++++++++

.. Note::

	**create a ReadTheDocs account**

	#.	go to https://readthedocs.org/, click ``Sign up`` (or, if you already have a *ReadTheDocs* account, skip the Sign up and log in); 
	#.	create an account; 
	#.	sign in.

.. Attention::

	*ReadTheDocs* is free as long as your documentation can be **public**.  We will look at other options if we don't want public documentations later.

.. Note::

	**Set up a connected account**

	#.	once logged in, click the ``Connect your Accounts`` button; 
	#.	we are connecting to GitHub, so click the ``Connect to GitHub`` button; 
	#.	(if we are not logged into our GitHub account, then we may be prompted to sign into GitHub;)
	#.	we are directed to the GitHub connection consent screen.  Click the ``Authorize readthedocs`` button, the page will redirect to https://readthedocs.org; 
	
			ReadTheDocs wants to have certain access to our GitHub account to be able to grab content and monitor the repositories via web hooks, etc.

	#.	click on the name badge (top-right) to get to the ReadTheDocs account homepage; 
	#.	click the ``Import a Project`` button; 
	#.	we may be prompted to ::
			
			Import a Repository

				No remote repositories found, try refreshing your accounts.

		click the ``Refresh`` icon; 

	#.	click the ``Plus`` icon on the row containing the repository we want to Import; 
	#.	we can change the ``Name``, ``Repository URL``, and the ``Repository type`` of the Project; click ``Next``; 
	#.	we see the following: ::
		
			Webhook successfully added

				Your documentation is building
				You'll be able to view your documentation in a minute or two, once your project is done building.

		wait a minute or two, *refresh* the page; 

	#.	we see: ::
		
			Your documentation is ready to use

				Your documentation has been built. Ensure your documentation is kept up to date with every commit to your repository, by setting up a webhook.
		we're done for now.

Click the ``View Docs`` button (top-right), we can now see a public URL where our documentation project is published.  It looks something like: ::

	https://GitHubRepoNameHere.readthedocs.io/en/latest/index.html

We have now completed the one-time set up activities.

Continuous integration / continuous delivery
++++++++++++++++++++++++++++++++++++++++++++

We consider the following scenario:

	#.	contributors, developers, or authors make some kind of a check-in, commit, or change to a source control repository; 
	#.	the act of making a change to this source control repository would then automatically initiate a build process; 
	#.	the build process produces some artifacts or results of the build---in our case, this will be the ``.html`` and supporting files for the doc website; 
	#.	*if* this process of creating artifacts does not require any human intervention, other than to make the change to the source control, *then* we have continuous integration ("*CI*"); 
	#.	after a CI has been established, it's possible to recognise a new build artifact and automatically deploy those artifacts to a server that makes them available to end users---*if* this happens automatically without human intervention, *then* we have continuous delivery ("*CD*").

We can execute automated test within these processes, e.g. notifications, require approvals, etc.---The main point is that the heavy lifting of creating the builds and getting them deployed happens without human intervention, which is not labour intensive (other than the committing repository change).  We can focus on processes being initiated or approved.  We explore how to do this with out doc project.

Setting up CI/CD on ReadTheDocs
+++++++++++++++++++++++++++++++

What we need to enable CI/CD for our ReadTheDocs project is to enable the GitHub webhook for our doc project.

.. Note::

	**ReadTheDocs/GitHub webhook and pushing changes**

	#.	log into https://readthedocs.org; go to our doc project (name badge -> dropdown list -> My projects -> OurDocProjectHere); if we are on the correct page, then we will see the following: ::
		
			Your documentation is ready to use

				Your documentation has been built. Ensure your documentation is kept up to date with every commit to your repository, by setting up a webhook.

	#.	we view the ``Admin`` function by clicking that button; 
	#.	we see some default options when we set up the doc project here; go to the ``Integrations`` tab (left navigation page);
	#.	we see that ``GitHub incoming webhook`` is already set up.  
		*ReadTheDocs* sets up the ``GitHub incoming webhook`` for us when we connected out GitHub repository to this project.  Let's make a change and see what happens; 
	#.	make a change to one of our ``.rst`` files in the doc project (that is published on *ReadTheDocs*); save the change; 
	#.	write a ``Commit Message``, commit the change (``Ctrl + Enter``)
	
			we see that there is one uncommitted change under the ``Source Control`` tab (``Ctrl + Shift + G``).
		
			In fact, we can even see in the VS Code toolbar (bottom-left) that we:

				-	are in the master branch; 
				-	have zero remote changes that needs to be applied or pulled; 
				-	have one local change that needs to be pushed up to the remote repository; 
	
	#.	click the ``...`` icon under the ``Source Control`` tab to see ``More`` options; 
	#.	choose ``Push`` to push the changes from our local version up to the remote repository; 
	
We have just pushed our change into GitHub, so let's go back to our ReadTheDocs project page.  Refresh the page: ::

	Your documentation is building

	You'll be able to veiw your documentation in a minute or two, once your project is done building

wait for the build to finish and ::

	Your documentation is ready to use

	Your documentation bas been built.  Ensure your documentation is kept up to date with every commit to your repository, by setting up a webhook.

click the ``Builds`` button on the project page, and we should see all the builds of the documentation.  Click the ``View Docs`` button (top-right) to see our change.
	
.. Attention:: **Git push and ReadTheDocs workflow summary**

	#.	we make a change on our local repository; 
	#.	we save and commited the change; 
	#.	we push our change into the master branch on GitHub; 
	#.	*ReadTheDocs* builds and deploys the project; 

We see the ``Edit on GitHub`` link on our current *ReadTheDocs* pages (top-right).  Click on ``Edit on GitHub``, and we are taken to the ``.rst`` file for that page on GitHub.  We can directly edit this file (click the ``Edit`` icon) on GitHub, and even commit the change (write a ``Commit Message``, click the ``Commit changes`` button, bottom).

Go back to the doc project Builds page on ReadTheDocs, and we can see an ``installing`` build that's being deployed on ReadTheDocs.  Once deployed, the build status changes to ``Passed``.  We can ``View Docs`` to verify that the committed changes have been deployed as well.  

.. Danger:: **Edit on GitHub**

	What we've just done above shows that *anyone* with a GitHub account can commit changes to the master branch right now *without* any review (or permission) from us.  

This may not be what we want, so we use pull requests.

Pull requests
+++++++++++++

We consider the following scenario:

	#.	we start with an existing repository, a ``master`` branch of the source code, and the owner, review, or creator (call her the **owner**) of the said repository; 
	#.	we have another person (call her the **contributor**) who has a feature they want to contribute; 
	#.	they have created their own branch (call it ``snf``) where they have done some work and want to get ``snf`` merged into the main master branch; 
	#.	they commit the changes made onto ``snf``, push it into the ``snf`` branch and the remote repository; 

To get ``snf`` merged into ``master``, they create what's called a **pull request**.

.. Note:: **Pull request workflow*
	
	-	the contributor submits a pull request ("*PR*") to the owner; 
	-	the PR prompts the owner to review their code; 
	-	the PR highlights the changes between the ``snf`` and ``master`` branches; 
	-	if the owner is happy with the code changes, then she can merge the changes into master---this is a **pull operation**, where the code differences are being pulled from ``snf`` into ``master``

PRs can come with *notifications*; PRs processes can also have conditional *policies*, e.g. branch merging needs two persons to approve before committing and merging.

We have demonstrated above that anyone with a GitHub account can commit changes to the ``master`` branch in our repository without our permission.  We change this so that to introduce a change, we need to do it via a pull request.

Configure GitHub to require Pull requests to Master
+++++++++++++++++++++++++++++++++++++++++++++++++++

Log into our GitHub account; go to our doc project remote repository.  We look at the ``Code`` tab (top-left).

.. Note:: **Set up PRs on GitHub for the protected branch**

	#.	go to the ``Settings`` tab; 
		
		.. Attention::

			It's worth our time to explore around the ``Settings`` on offer.  We focus on setting up PRs below.

	#.	click on the ``Branches`` node (left nav. pane); 
	#.	go to the ``Protected branches`` section; ``Choose a branch...``, select ``master``.  We see some options to protect the branch; 
	#.	check ``Protect this branch``, which will light up the succeeding options; 
	#.	for our purpose, we want every change to come from a PR, even from the repository *administrators*, check:
	
		#.	``Require pull request reviews before merging``; 
		#.	``Include administrators``;
		
	#.	``Save changes``; 

	We see a note that ::

		Branch protection options saved

Let's verify.

.. Attention:: **Changes to a protected branch on GitHub**

	#.	log into our GitHub account; open the doc project remote repository; ``Code`` tab; 
	#.	open a ``.rst`` file; 
	#.	click on ``Edit``; make an edit; 
	
	We see on the bottom that ::

		You can't commit to [master] because it is a protected branch.
		Create a new branch for this commit and start a pull request.

	and that what was the ``Commit changes`` button is now ``Propose file change``.  This means that the only option is to create a new branch and start a pull request.

	We can ``Cancel`` making the change.

.. Attention:: **Changes to a protected branch on vsc**

	#.	open *vsc*; 
	  	
	  	the status bar may show that there are changes on the remote repository that does not reflect locally.  *If* so, *then*: 

	  	#.	go to the ``Source Control`` tab (``Ctrl + Shift + G``); 
	  	#.	``More``; 
	  	#.	``Pull``; 
	  	
	  	.. Attention::

	  		Don't confuse the ``Pull`` operation with a PR:

	  		-	the ``Pull`` operation is the local code editor *pulling* the latest changes from the remote repository (currently on the ``master`` branch); 
	  		-	a PR is the workflow defined above (reviews and merging).
	
	#.	make a change and save it (or, if you already have changes that needs to be committed); 
	#.	``Commit`` locally; 
	#.	``Source Control``; ``More``; ``Push``; 
	
		we run into an error message: ::

			Can't push refs to remote.  Try running 'Pull' first to integrate your changes.

		This is a bit misleading:  trying a ``Pull`` will not help in this case.

	#.	``Open Git Log``; 
	  	
	  	we note the following lines: ::

	  		> git push origin master:master
			remote: error: GH006: Protected branch update failed for refs/heads/master.        
			remote: error: At least 1 approving review is required by reviewers with write access.        
			To https://github.com/GitHubAccountNameHere/GitHubRepoNameHere.git
			 ! [remote rejected] master -> master (protected branch hook declined)
			error: failed to push some refs to 'https://github.com/GitHubAccountNameHere/GitHubRepoNameHere.git'

		which means that we're attempting to push a commit into a protected branch, which requires at least one reviewer.  This is exactly what we wanted.

.. Note::  **Undo a commit in vsc**

	#.	``Source Control``; 
	#.	``More``; 
	#.	``Undo Last Commit``; 
	
	which will make our changes pending again, ready for a commit.

.. Note::  **Discard a change in vsc**

	#.	``Source Control``; 
	#.	``CHANGES`` node; 
	#.	(hover over the file we intend to discard the changes on) ``Discard Changes``; 
	
	and to discard all changes made:

	-	(hover over the ``CHANGES`` node) ``Discard All Changes``.

Submit a Change via a Pull request
++++++++++++++++++++++++++++++++++

We cover the following:

	#.	create a branch or fork; 
	#.	make changes; 
	#.	commit changes; 
	#.	publish to the remote branch; 
	#.	create PR.

.. Note::  **Create a New Branch in vsc**

	#.	click the ``Branch`` icon on the Source Control status bar (bottom); 
	#.	``+ Create new branch``; 
	#.	name the branch (e.g. ``twig``); 
	#.	``Enter``.
	
	The status bar now shows ``twig`` as the current branch.  The Cloud upload icon means that the ``twig`` branch doesn't exist remotely in our GitHub repository yet.

We make a change to any ``.rst`` file (or, if we already have a change ready to commit, then), ``Commit``.  Remember, this is still a local commit in our ``twig`` branch.

.. Note::  **Publish a Branch onto GitHub in vsc**

	#.	``Source Control``; 
	#.	``More``; 
	#.	``Publish Branch``.

We go to GitHub.  Inside our doc project repository, we see the banner ::

	Your recently pushed branches:
	twig (x minute ago)			Compare & pull request

which is what we wanted.

.. Note:: **Open a pull request on Github**

	#.	go to GitHub doc project repository;
	#.	click ``Compare & pull request``; 
	#.	*(change the PR title)*; 
		
			*(the title of the PR defaults to the* commit message *we made before pushing the* ``twig`` *branch---we can change this if we want to)*; 

	#.	write a description
	
			adding some rationale or justification about why we are submitting the PR will give a reviewer with a better context of what they are reviewing and why we are suggesting the change; 

	#.	``Create pull request``.
	
	We see the PR and note the following: ::

		Add more commits by pushing to the twig branch on GitHubAccountNameHere/GitHubRepoNameHere

			Review required
			At least 1 approving review is required by reviewers with write access.

			Merging is blocked
			Merging can be performed automatically with 1 approving review.


Approve and Merge the Pull request
++++++++++++++++++++++++++++++++++

In this section, we will need at least one person with a GitHub account to act as a collaborator/reviewer.  Find a friend (or, if you're ``#foreveralone``, create another GitHub account).

.. Attention:: 

	As the owner of our doc project remote repository, by definition we're also an administrator, and we're not allowed to review our own PRs on GitHub.  This is a good thing.

If we don't have a reviewer, we would need to remove the option about including administrators and override some red warning about merging our own code.

.. Note::  
	**Adding a collaborator on GitHub**

	#.	log into our GitHub account, go to ``Settings``, ``Collaborators`` node; 
	#.	(if the collaborator is on GitHub) ``Search by username, full name or email address``
	#.	``Add collaborator``.
	
		The collaborator will receive an email inviting them to collaborate on the repository; accept the invitation.

.. Note::
	**Reviewing PRs as a collaborator on GitHub**

	#.	log in as a collaborator; 
	#.	go to the remote repository owner's repository URL; 
	#.	``Pull requests`` tab; 
	  	
	  		we see the following: ::

				Review required
				At least 1 approving review is required by reviewers with write access.

				Merging is blocked
				Merging can be performed automatically with 1 approving review.

	#.	``Add your review``; 
	
			we are taken to the GitHub text editor in browser, and note the following: 

				-	``Changes from [all commits]`` means that we're currently viewing a consolidated file of aggregated change commits PR'd in this branch; 
				-	when hovering over each line, we can comment by pressing the ``[+]`` icon; 
				-	click ``Review changes`` button, and we can:
					
					-	``Comment``; 
					-	``Approve``; 
					-	``Request changes``.
			
			In this example, we simply accept all commit changes, so:

	#.	click ``Review Changes``; check ``Approve``; click ``Submit review``.
	
	.. Attention::
	
		We see that the previously red notes are now green: ::

			Changes approved
			1 approving review by reviewers with write access.

			This branch has no conflicts with the base branch
			Merging can be performed automatically.

		When setting up PR conditions initially, we've only set the no. of approving reviews to 1, hence the trigger.

Log in as the owner of the remote repository, go to repository, ``Pull requests`` tab, click PR name (``twig`` in this case).  We see some tabs under it:

	-	``Conversation``
	 	
			gives an overview on the review process; 

	-	``Commits``
		
			lists the no. of commits the PR contains; 

	-	``Checks``; 
	-	``Files changed``
			
			gives the aggregate code view before and after the commit(s).

.. Note::

	To merge the PR branch with the base branch, 

		#.	press ``Merge pull request``; 
		#.	make a comment; 
		#.	``Confirm merge``.
		
		We are prompted with: ::

			Pull request successfully merged and closed
			You're all set-the [twig] branch can be safely deleted.

We can verify our changes on *ReadTheDocs* as well.

Summary
+++++++

We
	#.	created a Git repository on GitHub; 
	#.	hosted docs on ReadTheDocs; 
	#.	set up CI/CD; 
	#.	required PRs; 
	#.	executed PR workflow; 