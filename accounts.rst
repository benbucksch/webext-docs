========
accounts
========

This is preliminary documentation for the accounts API being developed in `bug 1488176`__.

__ https://bugzilla.mozilla.org/show_bug.cgi?id=1488176

Permissions
===========

- accountsRead

.. note::

  The permission ``accountsRead`` is required to use ``accounts``.

Functions
=========

.. _accounts.list:

list()
------

Returns all mail accounts.

Returns a `Promise`_ fulfilled with:

- array of :ref:`accounts.MailAccount`

.. _accounts.get:

get(accountId)
--------------

Returns details of the requested account, or null if it doesn't exist.

- ``accountId`` (string)

Returns a `Promise`_ fulfilled with:

- :ref:`accounts.MailAccount`

.. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

Types
=====

.. _accounts.MailAccount:

MailAccount
-----------

object

- ``folders`` (array of :ref:`accounts.MailFolder`)
- ``hostName`` (string)
- ``id`` (string)
- ``name`` (string)
- ``type`` (string)

.. _accounts.MailFolder:

MailFolder
----------

A folder object, as returned by the ``list`` and ``get`` methods.

object

- ``accountId`` (string)
- ``path`` (string)
- [``name``] (string)
