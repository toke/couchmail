couchmail basic mail handling tools for couchdb
===============================================

Abstract
--------

couchmail is an project for storing and accessing mails in couchdb
for archiving and accessing. Currently the prototype just tries to
implement import of Maildir archives to couchdb using the Python
programming language. Later this might be changed to run on node.js.
But no desicions are made yet. At the moment it acts as a sandbox
for playing with mails in couchdb.


Status
------

This project is an experiment. This document is an draft and may act
as an implementation guide or an idea pool.


Basic goals
-----------

 * Bulk Mail import
 * Standard JSON format
 * Simple mail web frontend
 * Basic statistic tools
 * Basic mail accessing JS library
 * Being a platform for experiments
 * Experiment with `_id` handling
 * Experiment with threading
 * Experiment with data mining and content linking


Dependencies
------------

Beside that this may subject to rapid changes I want to keep
the dependency list up to date.

 * Python 2.6
 * couchdb
 

Mail import
-----------

The basic feature of *couchmail* is to import message archives to
CouchDB. The importer can be used to import your existing mailboxes
to CouchDB.

Planned Bulk Connectors:

 * Maildir (needs work)
 * mbox (not implemented yet)
 * IMAP (not implemented yet)

Additionally there should be an SMTP sink in a way that can be
connected to an MTA like exim or postfix to deliver E-Mail to
couchmail.


Web Interface
-------------

Mails should be browsable via web. For bulk mailing lists and bulk
archives a threaded view should be the default. Since one of the
goals of couchmail is the standardisation of the JSON format
additional frontends should be possible. There should be a simple
JS library for accessing the stored mails. 


Mail output
-----------

A future goal of couchmail is to implement an IMAP frontend. This can
be used to access the stored mail with any IMAP capable Mail client
like mutt, thunderbird etc.


Misc
----
 * https://gist.github.com/806797
 * https://github.com/theodoreb/couchdb-maildir-fuse
 * http://www.reddit.com/r/programming/comments/fddnd/a_work_in_progress_experimenting_with_couchdb_as/
 * http://web.archiveorange.com/archive/v/cXBGjJytnclaPITmbsb2
 * http://www.mail-archive.com/couchdb-user@incubator.apache.org/msg02025.html
