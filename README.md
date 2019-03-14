# IOReg: Individual Organism Registry

## Purpose

__IOReg__ attempts to provide a mechanism to register arbitrary individual organisms of any given species, for the sake
of providing a universal, unique ID (in the form of a [UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier)) to that
individual.

The hope is to allow each individual organism to be referenced consistently across multiple applications and datasets.  Yes, this is
a pretty ambitious/crazy goal.


## Overview ##

Within a participating application, an IOReg-registered ID should act as an external, secondary ID for an individual organism.
It likely should _not_ play the role of a primary key, as it may change (see: **merging** below).  The IOReg ID is meant to
"tie together" disparate data sets via the common organism.

IOReg aims to be indifferent to method and accuracy of organism identification and matching; it merely represents and tracks changes.
Toward this end, it is proposed that `git` be used as a method to track changes in data, which will be in the form of JSON files,
with _each taxonomy in its own repository_.
Further, **GitHub** will act as the central repository of the (open) data.  Functionality can be embedded in applications using
libraries like [JGit](https://www.eclipse.org/jgit/) or [GitPython](https://github.com/gitpython-developers/GitPython), etc.


### Example ###

Assume two hypothetical applications/databases, **App-A** and **App-B**, which (in some way) reference individual humpback whales
(_Megaptera novaeangliae_).  App-A may contain an entry for, say, whale A-137; while App-B may know a whale nicknamed "Splashy"
(with an internal ID of 54321).

#### Register with IOReg ####

Under the current proposal, the [ITIS](https://itis.gov/) Taxonomic serial number for _Megaptera novaeangliae_ is used: **180530**.
App-A generates a random (version 4) UUID for A-137.  App-B generates one for Splashy.  Both add these as new entries under the
**180530 git repo**, which is later pushed to master on github.

#### Merging ####

Unless two applications _know ahead of time_ they are referencing the same organism
(and thus use the same UUID as IOReg ID, via some mechanism),
most contributions will consist of adding of _new individuals_.  However, at some point, it will be discovered that, within IOReg,
**two individuals are actually in fact the same individual**.  In this case, the organisms must be _merged_.  The party which made
the discovery does this by choosing one of the duplicate entries to remain
and codifying the change (again via JSON) under the ID which will
be getting deprecated.  Basically this tells participating appliations/databases that they should update their records to reflect
this change.  This may be (usually?) as simple as replacing the ID, however, more complicated issues can arise, such as a change
in taxonomy ("hey, it wasn't a humpback after all!"), etc.

In our example, if some third party discovers that Splash and A-137 are the same whale, one of the corresponding entries within
IOReg will be "retired", with JSON designating the other ID as the merged replacement.  This change is made via commit and
push in git.

#### Splitting ####

The discovery that a "single" individual IOReg ID, in fact, represents _two (or more) individuals_ -- aka **splitting** -- currently
will not be represented in IOReg.  _This may change over time as need arises._  Under the present proposal, the source
which discovered their (internal) split should simply register the new individual via IOReg as a normal new entry.

## Accuracy / Validation / Control ##

The validity and "approval" of changes to IOReg data is (intentionally) outside of the scope of the IOReg design.
It is hoped that **policy and procedure can be developed as needed** to address these issues, and likely will vary greatly
depending on species, usage, and many other factors.  The hope here is to provide a **technical mechanism** to reference
changing data and track (in detail) what changes are made.


## Technical Details

_Not yet finished._
