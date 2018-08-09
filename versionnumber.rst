****************************************************************
Project version numbering system
****************************************************************

Project level specification 
================================================================

We use the following convention

(<``DocType``>)<``Approved``>.<``StructuralChangeDraft``>.<``EditorialDraft``>

and use a ``v`` prefix in front of the version string to denote *version*.

.. Attention::

	Strings enclosed by parentheses ``( )`` are optional.

<``DocType``> (optional) (WIP)
----------------------------------------------------------------

<``Approved``>
----------------------------------------------------------------
	
The most recent final project version that has been approved by one or more persons.  Subsequent drafts are made upon the current version.  E.g. the first final version is ``v1.0.0``, and we work upon ``v1.0.0`` towards ``v2.0.0``.

When the working draft on the current final version has been approved, increase the version number by 1.0.0 and zero ``StructuralChangeDraft`` and ``EditorialDraft``.

Example: we submit ``v1.3.1`` for final approval; this is approved as the new final version.  Change ``v1.3.1`` to ``v2.0.0``.


<``StructuralChangeDraft``>
----------------------------------------------------------------

The project undergoes significant structural change.  E.g. Architectural change on Directories, adding/removing entire Directories, long-lived branch amendments.

When submitting a project structural change, increase the version number by 0.1.0 (and do not amend ``EditorialDraft``)

Example: we submit a structural change on ``v1.3.1``; this is approved.  Change ``v1.3.1`` to ``v1.4.1``.

<``EditorialDraft``>
----------------------------------------------------------------

Under the project, we make editorial changes (e.g. renaming documents, adding/removing/archiving documents).

When the editorial draft has been approved, increase the version number by 0.0.1.

Example:  we submit a structural change on v2.0.0; this is approved.  Change ``v2.0.0`` to ``v2.0.1``.

Document level specification 
================================================================

A similar convention can be applied at a document level

<``Approved``>
----------------------------------------------------------------

The most recent final document version.  We work upon this towards the next final version.

<``StructuralChangeDraft``>
----------------------------------------------------------------

The Document undergoes structural change at the ``parts``, ``chapters``, and ``sections`` level.

<``EditorialDraft``>
----------------------------------------------------------------

We make editorial changes to the document (e.g. spelling, punctuation, subsection items).

Filename convention 
================================================================

We use the following convention

(<``IterationCode``>_)<``Approved``><``StructuralChangeDraft``><``EditorialDraft``><``Procedure``>

.. Attention::

	Strings enclosed by parentheses ``( )`` are optional.

<``IterationCode``> (optional)
----------------------------------------------------------------

We assume a maximum of 99 changes at each version level, i.e. ``v0.0.0`` to ``v99.99.99``.  If any version level exceeds 99 changes, then assume another 99 iterations (or 99 \* 99 = 9,801 total changes) at the same version level.  

The ``IterationCode`` is six digits long, where

	#.	the first and second digits denote the number of ``Approved`` iterations; 
	#.	the third and fourth digits denote the number of ``StructuralChangeDraft`` iterations; 
	#.	the fifth and sixth (last) digits denote the number of ``EditorialDraft`` iterations.

Where present, the ``IterationCode`` is separated from the version number by an underscore ``_``.

E.g. 

	#.	``v99.0.1`` can change to ``v010000\_0.0.1``; 
	#.	``v3.99.4`` can change to ``v000100\_3.0.4``; 
	#.	``v2.5.99`` can change to ``v000001\_2.5.0``.

If the changes exceeds all 99 iterations, then increase the ``IterationCode`` length to 9 digits (and assume a maximum of 999 iteration changes), and so on.

E.g. 

	#.	``v990000\_99.1.2`` can change to ``v100000000\_0.1.2``.

Version level number 
----------------------------------------------------------------

Remove the period delimiter separating the version levels when writing it in a filename.  If the version level number is between 0 to 9 inclusive, then add a leading zero.  

The version level number is six digits long, where

	#.	the first and second digits denote the number of ``Approved`` changes; 
	#.	the third and fourth digits denote the number of ``StructuralChangeDraft`` changes; 
	#.	the fifth and sixth (last) digits denote the number of ``EditorialDraft`` changes.

E.g. 

	#.	``v1.0.0`` maps to ``v010000``; 
	#.	``v2.1.13`` maps to ``v020113``; 
	#.	``v11.0.1`` maps to ``v110001``.

<``Procedure``> suffix
----------------------------------------------------------------

The ``procedure`` suffix denotes the procedure the project/document has been sent on.

.. csv-table::

	:header: "Letter","Process"

	"a","approval needed"
	"c","consultation"
	"p","publication"
	"w","*work in progress*"

.. Attention::

	Add suffix ``letters`` to denote ``processes`` where appropriate.