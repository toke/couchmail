JSON format
===========

This document is an working draft for implement an JSON mail
storage format especially for CouchDB. It is work in progress.

Problems to solve
-----------------

 * Addressing issue how to construct and build unique `_id`?
 * Threading
 

The `_id` issue
---------------

*Problem:* when bulk importing we need a way to prevent duplication
of messages and a way to reference existing mails within threads.
The second can be done later via an view referencing the message-id.
Using the message-id itself is not URL-safe and some messages may
not have an unique message-id. Since the message-id can be generated
by the sender it´s usage as an unique document-id is not safe.
Using just random ID´s makes it hard to test for existing messages
and linking to them without querying the database.
For bulk import we can maybe rely on the unique IDs and other
header fields for generating an message id - like the filename or
id of an Maildir message or an IMAP id. Merging messages from two
different sources is not possible by this aproach.
When implementing different threading solutions the messages must
reference parent messages. In the mail header this is done by the
message-id. So we can write a view and build this thread there.

Various sources for the document-id:
 * Using the message-id as source
 * Using an random-id (like the couchdb-uuid)
 * Using an upstream-id like the Maildir-id or IMAP-uid
 * Building an own id by different header fields
 * Using an hash value of the full message or full header

In the demo-application we would like to use the message-id or/and
the upstream-id as a source to an sha1. Do we need something like
merging a secret for this too?


Root Keyspace
-------------

    '_id': '' /* Document ID need some rethinking */
    'type': 'couchmail/email'
    'version': '0.1a'
    '_debug': { /* Place for optional debugging Information */ } 
    'header': { /* Serialized mail headers */ }
    'meta': { /* Additionally information (size, link to _attachments,
                 threading information) */ 
    }
    'body': {
        'plain': '' /* plain text version of the e-mail rendered
                       at import time */
    }

meta Keyspace
-------------

We are not sure how to handle header fields right now (what to store
and how to serialize etc.) as long this is not clear we store some
of this important fields in the meta keyspace.
These include:
 
 * From ["",""]
 * To [["",""]…]
 * CC [["",""]…]
 * Sender ""
 * Date ""?
 * Subject ""
 * Delivered-to [""]
 * References/in-reply-to ? 

Design decisions:
We use arrays and arrays of arrays to store From, To, CC, etc to find
a good balance of usability and storage.


Handling header fields
----------------------

Should the header fields stored in the root 'header' key be normalized?
Should we store some of the key 'header' fields like from, to, subject,
date… in an normalized way under the 'meta' key? Do we store the raw
header somewhere - like an attachment? If we do store the header in an
attachment, then how can we access it later via view (see attachment
handling).


Attachment handling
-------------------

CouchDB attachments are used to store the raw body and the optional
mime parts of the message. If the raw header will be stored in an 
attachment too is not yet decided (see Handling header fields).

