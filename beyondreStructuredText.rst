.. ===	Beyond reStructuredText
	+++	Introduction
		Custom CSS
		Why Custom CSS
		Add Custom CSS to the Project
		Add markdown support and a markdown document
		Versions
		Enable versions with a long-lived branch
		Verify version behaviour
		Summary

Beyond reStructuredText
=======================



Introduction
++++++++++++

We have just learned about the ReadTheDocs platform, using reStructuredText, and setting up workflow with automated CI/CD using the GitHub and ReadTheDocs integration.  This is enough to get us started in creating our docs, but sometimes presentation matters, so we attempt to address some rudimentary issues here.

We will:

	-	add custom CSS; 
	-	enable markdown usage; 
	-	add support for different versions.

Custom CSS
++++++++++

We will add a custom CSS file into our project and
	
	-	discuss why we might want one; 
	-	create a custom stylesheet; 
	-	include it in the build process; 
	-	reference classes via the ``class`` directive.

We will cover one specific example of CSS styling; this *Document* does not attempt to cover CSS comprehensively.

Why Custom CSS
++++++++++++++

We imagine a scenario where we want to add a new column to a comparison table that contains a description of the items.

Our commits require PRs now, so we create a new branch (e.g. ``tableversion``), and we consider the following ``csv-table``: ::

	.. csv-table:: Table2
		:header: "entryID","variable1","variable2","variable3","variable4","variable5","variable6"

		"entry1","1","a","string1","option1","US","Quid igitur est? "
		"entry2","2","b","string2","option2","GB","inquit; audire enim cupio, quid non probes. "
		"entry3","3","c","string3","option3","CH","Principio, inquam, in physicis, quibus maxime gloriatur, primum totus est alienus. "
		"entry4","4","d","string4","option1","NL","Democritea dicit perpauca mutans, sed ita, ut ea, quae corrigere vult, mihi quidem depravare videatur. "
		"entry5","5","e","string5","option2","CN","ille atomos quas appellat, id est corpora individua propter soliditatem, censet in infinito inani, in quo nihil nec summum nec infimum nec medium nec ultimum nec extremum sit, ita ferri, ut concursionibus inter se cohaerescant, ex quo efficiantur ea, quae sint quaeque cernantur, omnia, eumque motum atomorum nullo a principio, sed ex aeterno tempore intellegi convenire. "
		"entry6","6","f","string6","option3","DE","[18] Epicurus autem, in quibus sequitur Democritum, non fere labitur. "

.. csv-table:: Table2
	:header: "entryID","variable1","variable2","variable3","variable4","variable5","variable6"

	"entry1","1","a","string1","option1","US","Quid igitur est? "
	"entry2","2","b","string2","option2","GB","inquit; audire enim cupio, quid non probes. "
	"entry3","3","c","string3","option3","CH","Principio, inquam, in physicis, quibus maxime gloriatur, primum totus est alienus. "
	"entry4","4","d","string4","option1","NL","Democritea dicit perpauca mutans, sed ita, ut ea, quae corrigere vult, mihi quidem depravare videatur. "
	"entry5","5","e","string5","option2","CN","ille atomos quas appellat, id est corpora individua propter soliditatem, censet in infinito inani, in quo nihil nec summum nec infimum nec medium nec ultimum nec extremum sit, ita ferri, ut concursionibus inter se cohaerescant, ex quo efficiantur ea, quae sint quaeque cernantur, omnia, eumque motum atomorum nullo a principio, sed ex aeterno tempore intellegi convenire. "
	"entry6","6","f","string6","option3","DE","[18] Epicurus autem, in quibus sequitur Democritum, non fere labitur. "

We can see a pretty long scroll bar below the table; the viewers will have to scroll right to have a look at the content we created.  It is not the most obvious looking scroll bar either, and forcing the content to remain on the page shouldn't hurt the overall flow.  We want to change the formatting so that the table remains inside the page width itself.  Specifically, we want to define a styling under a CSS file, include it in the build process, then reference the CSS class we create on our table (so the text wraps in a cell, for instance).

Add Custom CSS to the Project
+++++++++++++++++++++++++++++

Our first step in including some custom CSS in our project is to add a file containing the CSS to the ``_static`` directory.  In this example, we add a directory called ``css``, then a file called ``custom.css``.  

We paste in the CSS code, which has the inline style and a class that can be applied to table cells: ::

	.tight-table td{
		white-space:normal !important; 
	}

To include this in the build process, we open conf.py, and under Options for HTML output (for easy reference), we add: ::

	def setup(app):
		app.add_stylesheet('css/custom.css')

this defines the set up method and when the method gets called, it will add the stylesheet we created.  The add_stylesheet method will look in the _static directory as its starting location, and the build process automatically calls a set up method if we have one defined.  

We add the class reference to the same table pasted below: ::

	.. csv-table:: Table2
		:header: "entryID","variable1","variable2","variable3","variable4","variable5","variable6"
		:class: tight-table

		"entry1","1","a","string1","option1","US","Quid igitur est? "
		"entry2","2","b","string2","option2","GB","inquit; audire enim cupio, quid non probes. "
		"entry3","3","c","string3","option3","CH","Principio, inquam, in physicis, quibus maxime gloriatur, primum totus est alienus. "
		"entry4","4","d","string4","option1","NL","Democritea dicit perpauca mutans, sed ita, ut ea, quae corrigere vult, mihi quidem depravare videatur. "
		"entry5","5","e","string5","option2","CN","ille atomos quas appellat, id est corpora individua propter soliditatem, censet in infinito inani, in quo nihil nec summum nec infimum nec medium nec ultimum nec extremum sit, ita ferri, ut concursionibus inter se cohaerescant, ex quo efficiantur ea, quae sint quaeque cernantur, omnia, eumque motum atomorum nullo a principio, sed ex aeterno tempore intellegi convenire. "
		"entry6","6","f","string6","option3","DE","[18] Epicurus autem, in quibus sequitur Democritum, non fere labitur. "

the ``:class: tight-table`` directive sets the class value to the CSS class name as we previously defined in the CSS file (``.tight-table``), which looks like this:

.. csv-table:: Table2
	:header: "entryID","variable1","variable2","variable3","variable4","variable5","variable6"
	:class: tight-table

	"entry1","1","a","string1","option1","US","Quid igitur est? "
	"entry2","2","b","string2","option2","GB","inquit; audire enim cupio, quid non probes. "
	"entry3","3","c","string3","option3","CH","Principio, inquam, in physicis, quibus maxime gloriatur, primum totus est alienus. "
	"entry4","4","d","string4","option1","NL","Democritea dicit perpauca mutans, sed ita, ut ea, quae corrigere vult, mihi quidem depravare videatur. "
	"entry5","5","e","string5","option2","CN","ille atomos quas appellat, id est corpora individua propter soliditatem, censet in infinito inani, in quo nihil nec summum nec infimum nec medium nec ultimum nec extremum sit, ita ferri, ut concursionibus inter se cohaerescant, ex quo efficiantur ea, quae sint quaeque cernantur, omnia, eumque motum atomorum nullo a principio, sed ex aeterno tempore intellegi convenire. "
	"entry6","6","f","string6","option3","DE","[18] Epicurus autem, in quibus sequitur Democritum, non fere labitur. "

.. Attention::

	In *vsc* terminal (``Ctrl + '``), ``./make html`` to build the project, then open the ``.html`` file generated for this example under the ``_build`` directory to see the CSS applied.  

	The browser page should show the table with cell contents wrapped.

.. Attention::
	
	Our ``_build`` directory also contains ``/html/_static/css/custom.css``, and under ``_build/html/_static/css/``, there are also other CSS files, which came from the *ReadTheDocs.io* theme we applied.

.. Note::
	**Process to add a custom CSS in our repository**

		#.	add some inline styling into the css file we created; 
		#.	apply the class to the document elements we want.

Add *markdown* support and a *markdown* document
++++++++++++++++++++++++++++++++++++++++++++

We add support for *markdown* in our project so that we can use both ``.rst`` files and *markdown* (``.md``) files for our docs.  We refer to the *ReadTheDocs.io* **Getting Started** guide (https://docs.readthedocs.io/en/latest/getting_started.html), and go to the *In Markdown* section.

.. Attention::
	**ReadTheDocs prefers reStructuredText for technical documentation**
	
	Under the section, there is a note that while *ReadTheDocs.io* supports *markdown* "for basic prose content", "reStructuredText is the preferred format for technical documentation".  http://ericholscher.com/blog/2016/mar/15/dont-use-markdown-for-technical-docs/ gives some in-depth details.

.. Danger::
	
	This and other *Documents* in this project are written in *reStructedText*.  We will explore the **CommonMark** *markdown* flavour support here, but will not use it anywhere else.  The `blog post above <http://ericholscher.com/blog/2016/mar/15/dont-use-markdown-for-technical-docs/>`_ provides the following high-level reasons:

		#.	lack of specification and standards; 
		#.	non-uniform *markdown* "flavours" branches; 
		#.	lack of extensibility; 
		#.	lack of semantic meaning; 
		#.	lack of portability (into other languages).

.. Note::
	**Markdown setup**

	#.	open vsc terminal, run ::
			
			pip install recommonmark

	#.	add in ``conf.py`` the following: ::
			
			from recommonmark.parser import CommonMarkParser

			source_parsers = {
			    '.md': CommonMarkParser,
			}

			source_suffix = ['.rst', '.md']


	#.	we can now add files with the ``.md`` extension

.. Attention::

	This *Document* will not cover the *markdown* syntax.

Versions
++++++++

We look at version support in *ReadTheDocs.io*.  We may have a version in a production environment that is stable, but may also want to be communicating with a community about what's coming up or currently being reviewed and tested.  

We specifically look at this scenario by creating a release version of the documentation, as well as a latest version.  The latter documentation will refer to the features-in-development / being tested.

These version in ReadTheDocs.io are based on branches and/or tags we put onto commits.  We focus on branches below for simplicity.

.. Attention::  **ReadTheDocs.io behaviour driven by tags**

	refer here: https://docs.readthedocs.io/en/latest/versions.html

		The webpage describes how *ReadTheDocs.io* supports versions.

For our purposes, we will 

	#.	set up a long lived release branch in GitHub; 
	#.	use that branch as a version on *ReadTheDocs.io*; 
	#.	compare both versions on our doc site; 
	#.	verify version behaviour via PRs.

Enable versions with a long-lived branch
++++++++++++++++++++++++++++++++++++++++

.. Note::
	**Enable a version on ReadTheDocs**

	#.	create a ``release`` branch, in vsc, GitHub, or otherwise; 
	#.	go to *ReadTheDocs* project page, click ``Versions`` tab;
			
			We see that our ``release`` branch (in fact, *all* previous branches) are under ``Inactive Versions``.  We want to activate the ``release`` branch as a build.

	#.	click ``Edit`` on the ``Inactive Versions`` we should like to activate; 
	#.	check ``Active``; click ``Save``

We now have two active versions.  We can verify this by going to the ``Overview`` tab and seeing two ``Versions``: ``latest`` and ``release``; and under the ``Builds`` tab we can see a record of the ``version release``  build (distinct from the ``version latest`` build).

On the doc project webpage, we can see the version on the bottom right.  Click the banner to switch versions and more options.


Verify version behaviour
++++++++++++++++++++++++

We now have two versions of our documentation.  We push distinct changes on the two distinct branches (``master`` vs ``release``) to verify that the versions behave appropriately.

.. Note::
	Verify CI/CD on version latest on ReadTheDocs

	#.	create a branch; 
	#.	commit some changes; 
	#.	PR; 
	#.	approve PR; 
	#.	Merge to ``master`` branch
	
	This will trigger an CI/CD process which automatically initiate a new build on the ``version latest`` documentation.

.. Note::
	**Verify CI/CD when merging latest version with release version**

	#.	create a new PR:  

			-	``base: release``; 
			-	``compare: master``; 
				
					this means we're merging changes committed in the compare ``master`` branch into the base ``release`` branch; 

					**NB** our ``release`` branch is not protected
	#.	``Merge pull request``; 
	#.	``Confirm merge``
	
	This will trigger an CI/CD process which automatically initiate a new build on the ``version release`` documentation.  What we have effectively done is deploying our latest version (which contains additional/amended information) of the documentation into the release version (the last stable release) of the documentation.  The same concept applies to a code project.

Summary
+++++++

We:
	#.	added custom CSS support; 
	#.	added markdown support; 
	#.	added version support.

.. Attention::
	**doc project contribution workflow summary**

		#.	create a ``NewBranch``; 
		#.	make changes; 
		#.	commit changes; 
		#.	publish branch; 
		#.	make PR:
				#.	``base: master``; 
				#.	``compare: NewBranch``; 
		#.	approve PR; 
		#.	*if* ``NewBranch`` merged to ``master``, *then* CI/CD triggers on *RTD* and a new build triggers on ``version latest``; *else* ``NewBranch`` is an ``Inactive Version`` on *RTD*; 
	
	To deploy the ``latest`` changes into a ``release`` version
	
		#.	make PR:
				#.	``base: release``; 
				#.	``compare: master``; 
		#.	approve PR; 
		#.	if merge ``master`` branch with ``release``, then CI/CD triggers on *RTD* and a new build triggers on ``version release``.