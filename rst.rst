The reStructuredText markup syntax
++++++++++++++++++++++++++++++++++

Introduction
============

Having a documentation project is great, but not very helpful is we cannot utilise the different constructs of a language to help highlight important points and create some structure to the information we are trying to convey.

We cover:

	#.	the most commonly used *reStructuredText* syntax directives (*instructions*); 

			.. Attention::

				This document does not attempt to cover *reStructuredText* comprehensively.  Visit http://www.sphinx-doc.org/en/master/usage/restructuredtext/index.html for more information on the markup syntax.

	#.	the table of contents ("*TOC*") tree
	#.	utilise different page elements using *reStructuredText* directives; 
	#.	utilise hyperlinks

The *table of contents* tree and document sections
==================================================

The ``toctree``
---------------

We start with the *rtd* **Getting Started** guide (https://docs.readthedocs.io/en/latest/getting_started.html) and note its navigation pane:

	#.	the lightest coloured text is also the highest-level content header (``USER DOCUMENTATION``, ``ABOUT READ THE DOCS``, ``FEATURE DOCUMENTATION``, etc.)  Each one of these is a **table of contents tree** ("``toctree``"); 

			we can think of these ``toctree`` s as the most-major *topics* of the entire documentation project that separate the documentation.  Under each ``toctree``, we see further levels (and documents) all working towards the ``toctree`` topic.  

			Open ``Getting Started`` in the nav. pane under ``USER DOCUMENTATION``.

	#.	``Getting Started`` is the **heading** of a document---this is first level under the ``toctree``; 

			in *rST*, each one of these would have its own ``.rst`` file; and in the ``index.rst``, we can define the ``toctree`` s to direct their contents to each of the ``.rst`` files---this builds up the navigation panel.

	#.	``Write Your Docs`` is a **section** under the ``Getting Started`` document; 

	#.	``In reStructedText`` is a **subsection** under the ``Write Your Docs`` section.

It is good to have the end product in mind.  Imagine that we have to build a doc project using the following structure (levels separated by indent): ::

	USER DOCUMENTATION
		Getting Started
			Prerequisites
			Additional resources
		Examples
		Troubleshooting

	FREQUENTLY ASKED QUESTIONS
		What is love?
		Baby don't hurt me?
		Don't hurt me?
		No more?

This means we need to:

	#.	build two ``toctree`` s in ``index.rst``: 

			-	``USER DOCUMENTATION``; and
			-	``FREQUENTLY ASKED QUESTIONS``; 
		
	#.	write seven ``.rst`` files (each corresponding to a *title*); 
	#.	under (say) ``gettingstarted.rst``, create two *sections*: 

			-	``Prerequisites``; and
			-	``Additional resources``; 
		
	#.	reference the ``toctree`` s to the ``.rst`` files respectively.

In ``index.rst``, we can write the following: ::

	.. toctree::
	   :maxdepth: 2
	   :caption: USER DOCUMENTATION

	   gettingstarted
	   examples
	   troubleshooting

	.. toctree::
	   :maxdepth: 2
	   :caption: FREQUENTLY ASKED QUESTIONS

	   whatislove
	   babydonthurtme
	   donthurtme
	   nomore

.. Note::

	

.. Note::

	The strings under the ``toctree`` directives are file names, which makes the ``toctree`` look for the file name in the desired foler path.  In the example above, we might have a folder that contains:

		-	``gettingstarted.rst``
		-	``examples.rst``
		-	``troubleshooting.rst``
		-	``whatislove.rst``
		-	``babydonthurtme.rst``
		-	``donthurtme.rst``
		-	``nomore.rst``
	
	If we are referencing a file in a sub-directory under our doc project directory, then in the ``index.rst`` file we need to write out the full directory link under the ``toctree``.  For example, if ``gettingstarted.rst`` is located under the ``NewFolder`` directory, we have to write: ::

		.. toctree::
		   :maxdepth: 2
		   :caption: USER DOCUMENTATION

		   NewFolder/gettingstarted		(<- the file path)
		   examples
		   troubleshooting


.. Note::
	
	The ``maxdepth`` directive defines the deepest level we want our nav. pane to display.  Using the above example:

		-	if we define ``:maxdepth: 1``, then in the nav. pane we will only see ``Getting Started`` (a *heading*), but not ``Prerequisites`` (a *section*); 
		-	elseif we define ``:maxdepth: 2``, then we see both, with ``Prerquisites`` nested under ``Getting Started``.

.. Note::

	*ReadTheDocs* will ignore *empty* ``.rst`` files and will not include them in the build (nor link them in the nav. pane under the ``toctree``); the ``make`` html build command will not generate the respective ``.html`` files either.

Sections and headings
---------------------

Recall that we need to hypothetically implement this: ::

	USER DOCUMENTATION
		Getting Started
			Prerequisites
			Additional resources

We know that:

	#.	``USER DOCUMENTATION`` is a ``toctree``; 
	#.	we have a file called ``gettingstarted.rst``.

*ReadTheDocs* will generate the ``toctree`` nav. pane based on the **headers** and the **sections** (and every subsequent **sub-sections**) of each document.  

The **rST** syntax needs underlining (and optional overline) the section title with a punctuation character, *at least* as long as the text.

.. Note::

	Normally, there are no heading levels assigned to certain characters as the structure is determined from the seccession of headings. However, `the Python documentation <https://devguide.python.org/documenting/#style-guide>`_ suggests the following:

		-	``#`` with *overline*, for **parts**; 
		-	``*`` with *overline*, for **chapters**; 
		-	``=``, for **sections**; 
		-	``-``, for **subsections**; 
		-	``^``, for **subsubsections**; 
		-	``"``, for **paragraphs**.
	
	We can use a deeper nesting level, but keep in mind that most target formats (HTML, LaTeX) have a limited supported nesting depth.

Using the above example, we can do the following in ``gettingstarted.rst``: ::

	**********************************
	Getting Started
	**********************************



	Prerequisites
	==================================



	Additional resources
	==================================



Text formatting
===============

In any ``.rst`` file, enclose string by
	*	``*``, for *italic*; 
	*	``**``, for **bold**; 
	*	``````, for ``code`` (or ``verbatim``).

Lists
=====

Numbered lists
--------------------------------

A list of items each preceeded by ``#.`` will generate a **numbered list**.  For example: ::

	#. Item1
	#. Item2
	#. Item3

generates

#. Item1
#. Item2
#. Item3

Itemised lists
--------------------------------

A list of items each preceeded by either a ``-`` or a ``*`` will generate an **itemised list**.  For example: ::

	- Item1
	- Item2
	- Item3
	
	* Item4
	* Item5
	* Item6

generates

- Item1
- Item2
- Item3

* Item4
* Item5
* Item6

Nested lists
--------------------------------

We can nest lists within lists (numbered or otherwise), but they must be separated from the parent list items by blank lines.  For example: ::

	* this is
	* a list

	  * with a nested list
	  * and some subitems

	* and here the parent list continues

generates

* this is
* a list

  * with a nested list
  * and some subitems

* and here the parent list continues

Admonitions
===========

``Admonition`` in *rtd* comes in four flavours:

	#.	green; 
	#.	blue; 
	#.	yellow; and
	#.	red.

..	Attention::
	{
	``Attention``, 
	``Caution``, 
	``Warning``
	}

		| "Cowards die many times before their deaths;
		| The valiant never taste of death but once.
		| Of all the wonders that I yet have heard.
		| It seems to me most strange that men should fear;
		| Seeing that death, a necessary end,
		| Will come when it will come."

..	Danger::
	{
	``Danger``, 
	``Error``, 
	}

		| "Canst thou, O partial sleep, give thy repose
		| To the wet sea-boy in an hour so rude,
		| And in the calmest and most stillest night,
		| With all appliances and means to boot,
		| Deny it to a king? Then happy low, lie down!
		| Uneasy lies the head that wears a crown."

..	Hint::
	{
	``Hint``,  
	``Important``, 
	``Tip``
	}

		| "Doubt thou the stars are fire;
		| Doubt that the sun doth move;
		| Doubt truth to be a liar;
		| But never doubt I love."

..	Note::
	{
	``Note``
	}

		| "Henceforth I will not have to do with pity:
		| Meet I an infant of the house of York,
		| Into as many gobbets will I cut it 
		| As wild Medea young Absyrtus did: 
		| In cruelty will I seek out my fame. "

You can also make your own ``admonition``.

Images
======

You can link to an image in your folder using a relative directory path under your doc project directory, like so::

	..	image::	/images/201807181231_KJU_Serious.JPG

..	image::	/images/201807181231_KJU_Serious.JPG

Code Samples
============

Add a code-block by:

	#.	ending the current paragraph with two colons ``::``; 
	#.	indent the code one level down from your current paragraph; 
	#.	leave a line break one line above and one line below the enclosed code.
	
We can define the code-block language directive by ::

	.. code-block:: LanguageHere

to get better highlighting.

Tables
======

We note two types of tables, as they are the most user friendly:  ``list-table`` and ``csv-table``.


``list-table``
--------------------------------

Add a list table with title ::

	.. list-table:: Table1
		:widths: 20 30 40
		:header-rows: 1
		
		*	- entryID
			- variable1
			- variable2
		*	- entry1
			- 1.00
			- string1
		*	- entry2
			- 2.00
			- string2
		*	- entry3
			- 3.00
			- string3

.. list-table:: Table1
	:widths: 20 30 40
	:header-rows: 1
	
	*	- entryID
		- variable1
		- variable2
	*	- entry1
		- 1.00
		- string1
	*	- entry2
		- 2.00
		- string2
	*	- entry3
		- 3.00
		- string3

each asterisk ``*`` denotes one row, and the dashes ``-`` denotes the variables of that entry according to the headers.  The directive indent must match the table indent.

``csv-table``
--------------------------------

Or use the ``csv-table`` ::

	.. csv-table:: Table2
		:header: entryID,variable1,variable2,variable3,variable4,variable5
		:widths: 20 25 30 35 40 45

		entry1,1,a,string1,option1,US
		entry2,2,b,string2,option2,GB
		entry3,3,c,string3,option3,CH
		entry4,4,d,string4,option1,NL
		entry5,5,e,string5,option2,CN
		entry6,6,f,string6,option3,DE

.. csv-table:: Table2
	:header: entryID,variable1,variable2,variable3,variable4,variable5
	:widths: 20 25 30 35 40 45

	entry1,1,a,string1,option1,US
	entry2,2,b,string2,option2,GB
	entry3,3,c,string3,option3,CH
	entry4,4,d,string4,option1,NL
	entry5,5,e,string5,option2,CN
	entry6,6,f,string6,option3,DE

.. Note::

	The ``csv-table`` seems friendliest to *Sublime* and *Excel*.

Hyperlinks
==========

We discuss three ways of hyperlinking:

	#.	to an URL; 
	#.	to a document within the project; 
	#.	to a spot on a document within the project.

Hyperlink an URL
--------------------------------

An URL by itself will be retained as a hyperlink:  https://www.midpoint.com/home.

Otherwise, to add a URL hyperlink on some text:  ::

	`Midpoint homepage <https://www.midpoint.com/home>`_

Generates a link to the `Midpoint homepage <https://www.midpoint.com/home>`_.

URLs work on their own paragraphs:

https://www.midpoint.com/home

Hyperlink a document within the project
--------------------------------

To link to a target document, use ::

	:doc:`LinkDocumentFilePath`

For example: ::

	:doc:`acasefordoc`

returns

:doc:`acasefordoc`.

Hyperlink a spot on a document within the project
----------------------------------------------------------------

First, we need to tag the link spot (this is usually a secton title; cross-referencing a non-section-title locaton requires a different syntax): ::

	.. _TagNameHere:

For example, I placed ``.. _whyrtd:`` over the ``Why *ReadTheDocs*?`` section under ``acasefordoc.rst``

We reference this: ::

	:ref:`whyrtd`

which generates

:ref:`whyrtd`