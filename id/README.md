# IOReg Taxonomy ID Directories

For a general overview of the project, see the main README (link).

## Overview of the "id" directory

This directory will contain *one directory per __taxonomy__*, which will contain sub-directories for each __individual id__.

Taxonomy directories are named based on
**ITIS Taxonomic Serial Numbers** (<https://www.itis.gov>) and each will be a **git sub-module** that can be cloned
and updated as needed.

To populate specifics taxonomies, for example:
`git submodule init <taxonomy-directory-name>`, then
`git submodule update <taxonomy-directory-name>`.


## Contents of id directories

For an explanation of the contents of **id directories**, please see the Technical Overview document (link).
