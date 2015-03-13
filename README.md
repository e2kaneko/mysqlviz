mysqlviz
========

Render a graphical representation of a MySQL or SQLite database from a `mysqldump` or `sqlite3` `.dump` file.

News
----
 * 2013/09
    * Version 1.0 released:
       * Uses `/usr/bin/env/php` in shebang line to improve portability
       * Fixes new PHP versions' now-deprecated `split()` with `explode()`
       * Silences warnings on modern PHP default configurations related to array indices handling
 * ~2009
    * Version 0.3 released:
       * Now with sqlite support

Features
--------
 * Can infer foreign key relationships if you do not have them defined
 * Handles partial dumps (FK to tables that are not defined within the dump)
 * Fast!  Uses _sed_ and _grep_ for data extraction (MySQL only)


Example output
--------------
<img alt="Example" src="https://raw.githubusercontent.com/globalcitizen/mysqlviz/master/eg.png">

_This output was generated from the input file https://raw.githubusercontent.com/globalcitizen/mysqlviz/master/eg.sql._


Installation
============

FreeBSD
-------
`port install mysqlviz`

Ubuntu and variants
-------------------
`sudo apt-get install -y graphviz`

Then install code from here.

Gentoo and variants
-------------------
`sudo emerge graphviz`

Then install code from here.

Usage
=====

```
[mysqlviz - mysql + sqlite database visualisation tool]

usage:
  ./mysqlviz -f <sqldumpfile> [-r]
                                 ^--- 'redump' mode: generates a
                                      mysqldump command line to redump.
toolchain:
 $ mysqldump -d db >db.sql          # MySQL: -d = 'no data', only structure
    - OR -
 $ sqlite database.db .dump >db.sql # SQLite (also: 'sqlite3 ...')
 $ ./mysqlviz -f ./db.sql >./db.dot # 'dot' is a graphviz format.
 $ dot -Tpng db.dot >db.png         # generate image with graphviz

notes:
 if you do not have any foreign keys defined, relationships will be
 assumed in cases where a column name ends in one of (id/ID/_id/_ID) and
 there is a matching table (for example, onetable.othertable_ID column, and
 othertable is defined).  the program will also match tables with
 various prefixes and suffixes.
```

Dependencies
============
Written in PHP.  Uses `sed` and `grep` for speed, and `graphviz` as the graph renderer.  Tested with output from MySQL 5.0 and SQLite 3.7.2 on PHP v4.x through 5.4.x

Wishlist
========
 * Cutesy diamonds etc. to denote relationship types
 * Testing against dumps from older/newer MySQL versions (eg. MariaDB)
 * Options for modifying the complexity of output (column types, relationship type, etc.)
