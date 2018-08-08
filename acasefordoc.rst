..	+++	A case for documentation
		===	Overview
			Documenting our own software
			Documenting others' package
			Documentation options
			Why *ReadTheDocs*?
			Rest of the *documentation*

A case for documentation
++++++++++++++++++++++++

Documentation is rarely a first class citizen when it comes to software projects, but getting it done well can improve the usability and adoption of our project and enable us to move on more quickly to either the next features or the next project without getting bogged down in routine support of what we've just created and released.

In this *documentation*, we discuss how to build a documentation project from scratch and the Git-based workflow used for making contributions and changes to existing documentation on projects.

For the from scratch doc project, we will focus on a platform called *ReadTheDocs*.

The Git-based workflow will apply to most open source projects, whether they are using *ReadTheDocs* or not.  So whether we're a software author of a package needing documentation, or a consumer of an open source solution with some documentation gaps, this *documentation* may help you.

Overview
========

We discuss the following in this *documentation*:

	#.	why we should bother with documentation with respect to both authors and consumers; 
	#.	what our options are for documentations; 
	#.	why we should choose *ReadTheDocs*; 
	#.	what this *documentation* will attempt to cover.

Documenting our own software
============================

If we have written a software package or application that needs documentation, the reasons for creating good docs are compelling.

**We should document our own application because:**

	#.	it provides a better "out-of-the-box" experience post deployment; 
	
			with getting started information, we're providing a helping hand to new users who evaluates whether our package is worth using.  This is helpful even if they do not have a choice regarding whether or not to use our application.  Moreover, by going further than just a deployment; 

	#.	it encourages the use--**proper** use--of our application; 
	
			communicating standard flows and/or configurations to the end user can often be the difference between a successful and failed implementation---a user can never use an application wrongly; often it is a design/communication issue on a poorly documented/tested feature, and documentation with use cases, working examples, or deployment/development intentions can alleviate this; 

	#.	it avoids questions--**repeated** questions--on subjects covered in the documentation *and* saves us time; 
			
			if we provide answers in an easy to understand and well structured documentation, then it will help us quickly point support requests in the right direction.  It avoids both the human error/oversight in thinking up an answer on the spot--in having a single (but *living*) source of truth--and saves us time.

	#.	we do not want to be the *bottleneck*; 
			
			if development or **adoption** is conditional on getting answers from the owners of a project, then the owners are the bottleneck, because their speed of answer are the gating factor; if the adopters do not know what the new features are, then the new features will never be adopted.  However, if the answers are in the documentation, which the adopters trust and will refer to, then they can adopt new features / adjust workflow however quickly as they wish.

Documenting others' package
===========================

We may have reasons to document packages even if they are not ours.  This often comes in an open source package we want to use in our own applications.  If the final applications we write are used by others, then the argument for documentation is set out above.  However, if we have trouble adopting an open source package, we may want to help out.

**We may want to document others' package because:**

	#.	it "gives back" to the community; 
	  	
	  		the author(s) of the open source package created something that might be of benefit to us; by documenting on how we troubleshoot our implementation, or by improving upon the existing information, we're contributing to the original project; 

	#.	it helps others, like ourselves; 
	  	
			if we are having difficulty with a package, then chances are there are many like us having the same difficulty.  We can directly help them by adding some documentation; 

	#.	it improves the package; 
	  	
			having a better set of documentation encourages more adoption, which could help with additional development and contribution.

Documentation options
=====================

-	*Wiki*; 
	
		project wikis are available on many source hosting platforms, like GitHub, Bitbucket, and TFS.  These provide some good functionality, but there is no defined workflow involved for approving changes to the documentation.  It is either a free-for-all or limited to contributors on the project.  This can dissuade many would-be contributors from adding or improving the documentation we create; 

-	develop our own; 
		
		this is certainly an option that provides the maximum flexibility we might want, but it comes at the price of *reinventing the wheel* for many features available out-of-the-box from other solutions.  For example, we need to consider search, navigation, architecture, styling---time better used elsewhere.  Moreover, we may need to repeat this process if we have multiple projects that need distinct documentation; 

-	*DocFX*; 

		this might be a good option if we focus predominantly on ``.NET``.  This is what Microsoft has used to create the new docs on the Microsoft.com site.  The code generated is limited to ``C#`` and ``VB.net``, and uses a custom *markdown* format along the flavour used by GitHub.  This only generates the documentation site for us---we have to figure out the hosting ourselves; 

-	*ReadTheDocs*; 
 	
 		*(see next section.)*

Why *ReadTheDocs*?
==================

The `ReadtheDocs site <https://docs.readthedocs.io/en/latest/getting_started.html>`_ documents the *ReadTheDocs* platform and its many capabilities we will be leveraging in this *documentation*.  

It has:

	#.	an easy to use navigation section; 
	#.	a built-in search tool; 
	#.	code embedding using the reStructuredText markup syntax; 
		
			.. Tip::

				We can define the code-embedding syntax highlighting using the ``code-block`` directive.

	#.	different *admonitions* (see the post-it like *Tip* above---easy and eye-catching); 
	#.	a good mobile viewing UX.

All of these in-the-box features let s focus less on the mechanics, look, and behaviour of the documentation, and more on its contents.  Moreover, *ReadTheDocs* provides free hosting and automated integration with GitHub, GitLab, Bitbucket, or other ways.

Rest of the *documentation*
===========================

We will:

	#.	install some prerequisites; 
	#.	build a ReadTheDocs site locally; 
	#.	create some content using the *reStructuredText* markup syntax; 
	#.	establish and leverage a Git-based automated workflow for our documentation site updates; 
	#.	explore customisation beyond *reStructuredText*.

.. Attention::
	We will not assume any prior knowledge on any of the tools we will be using.  All examples are set up from scratch.