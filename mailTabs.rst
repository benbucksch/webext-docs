========
mailTabs
========

This is preliminary documentation for the mail tabs API being developed in `bug 1499617`__.

__ https://bugzilla.mozilla.org/show_bug.cgi?id=1499617

The `Filter`__  and `Layout`__ sample extensions use this API.

__ https://github.com/thundernest/sample-extensions/tree/master/filter
__ https://github.com/thundernest/sample-extensions/tree/master/layout

Permissions
===========

- mailTabs

.. note::

  The permission ``mailTabs`` is required to use ``mailTabs``.

Functions
=========

.. _mailTabs.getAll:

getAll()
--------

Returns an array of all mail tabs in all windows.

Returns a `Promise`_ fulfilled with:

- array of :ref:`mailTabs.MailTab`

.. _mailTabs.getCurrent:

getCurrent()
------------

Returns the current mail tab in the most recent window, or throws an exception if the current tab is not a mail tab.

Returns a `Promise`_ fulfilled with:

- :ref:`mailTabs.MailTab`

.. _mailTabs.update:

update([tabId], updateProperties)
---------------------------------

Modifies the properties of a mail tab. Properties that are not specified in ``updateProperties`` are not modified.

- [``tabId``] (integer) Defaults to the selected tab of the current window.
- ``updateProperties`` (object)

  - [``displayedFolder``] (object) Sets the folder displayed in the tab. The extension must have an accounts permission to do this.
  - [``folderPaneVisible``] (boolean) Shows or hides the folder pane.
  - [``layout``] (`string <enum_layout_4_>`_) Sets the arrangement of the folder pane, message list pane, and message display pane. Note that setting this applies it to all mail tabs.
  - [``messagePaneVisible``] (boolean) Shows or hides the message display pane.
  - [``sortOrder``] (`string <enum_sortOrder_6_>`_) Sorts the list of messages. ``sortType`` must also be given.
  - [``sortType``] (`string <enum_sortType_7_>`_) Sorts the list of messages. ``sortOrder`` must also be given.

.. _enum_layout_4:

Values for layout:

- ``standard``
- ``wide``
- ``vertical``

.. _enum_sortOrder_6:

Values for sortOrder:

- ``none``
- ``ascending``
- ``descending``

.. _enum_sortType_7:

Values for sortType:

- ``byNone``
- ``byDate``
- ``bySubject``
- ``byAuthor``
- ``byId``
- ``byThread``
- ``byPriority``
- ``byStatus``
- ``bySize``
- ``byFlagged``
- ``byUnread``
- ``byRecipient``
- ``byLocation``
- ``byTags``
- ``byJunkStatus``
- ``byAttachments``
- ``byAccount``
- ``byCustom``
- ``byReceived``
- ``byCorrespondent``

.. _mailTabs.getSelectedMessages:

getSelectedMessages([tabId])
----------------------------

Lists the selected messages in the current folder. A messages permission is required to do this.

- [``tabId``] (integer) Defaults to the selected tab of the current window.

Returns a `Promise`_ fulfilled with:

- :ref:`messages.MessageList`

.. _mailTabs.setQuickFilter:

setQuickFilter([tabId], properties)
-----------------------------------

Sets the Quick Filter user interface based on the options specified.

- [``tabId``] (integer) Defaults to the selected tab of the current window.
- ``properties`` (object)

  - [``attachment``] (boolean) Shows only messages with attachments.
  - [``contact``] (boolean) Shows only messages from people in the address book.
  - [``show``] (boolean) Shows or hides the Quick Filter bar.
  - [``starred``] (boolean) Shows only starred messages.
  - [``tags``] (boolean or :ref:`mailTabs.QuickFilterTagsDetail`) Shows only messages with tags on them.
  - [``text``] (:ref:`mailTabs.QuickFilterTextDetail`) Shows only messages matching the supplied text.
  - [``unread``] (boolean) Shows only unread messages.

.. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

Events
======

.. _mailTabs.onDisplayedFolderChanged:

onDisplayedFolderChanged()
--------------------------

Fired when the displayed folder changes in any mail tab.

.. note::

  The permission ``accountsRead`` is required to use ``onDisplayedFolderChanged``.

.. _mailTabs.onSelectedMessagesChanged:

onSelectedMessagesChanged()
---------------------------

Fired when the selected messages change in any mail tab.

.. note::

  The permission ``messagesRead`` is required to use ``onSelectedMessagesChanged``.

Types
=====

.. _mailTabs.MailTab:

MailTab
-------

object

- ``active`` (boolean)
- ``displayedFolder`` (accounts.MailFolder)
- ``folderPaneVisible`` (boolean)
- ``id`` (integer)
- ``layout`` (`string <enum_layout_23_>`_)
- ``messagePaneVisible`` (boolean)
- ``sortOrder`` (`string <enum_sortOrder_25_>`_)
- ``sortType`` (`string <enum_sortType_26_>`_)
- ``windowId`` (integer)

.. _enum_layout_23:

Values for layout:

- ``standard``
- ``wide``
- ``vertical``

.. _enum_sortOrder_25:

Values for sortOrder:

- ``none``
- ``ascending``
- ``descending``

.. _enum_sortType_26:

Values for sortType:

- ``byNone``
- ``byDate``
- ``bySubject``
- ``byAuthor``
- ``byId``
- ``byThread``
- ``byPriority``
- ``byStatus``
- ``bySize``
- ``byFlagged``
- ``byUnread``
- ``byRecipient``
- ``byLocation``
- ``byTags``
- ``byJunkStatus``
- ``byAttachments``
- ``byAccount``
- ``byCustom``
- ``byReceived``
- ``byCorrespondent``

.. _mailTabs.QuickFilterTagsDetail:

QuickFilterTagsDetail
---------------------

object

- ``mode`` (`string <enum_mode_28_>`_) Whether all of the tag filters must apply, or any of them.
- ``tags`` (object) Object keys are tags to filter on, values are ``true`` if the message must have the tag, or ``false`` if it must not have the tag. For a list of available tags, call the :ref:`messages.listTags` method.

.. _enum_mode_28:

Values for mode:

- ``all``
- ``any``

.. _mailTabs.QuickFilterTextDetail:

QuickFilterTextDetail
---------------------

object

- ``text`` (string) String to match against the ``recipients``, ``sender``, ``subject``, or ``body``.
- [``body``] (boolean) Shows messages where ``text`` matches the message body.
- [``recipients``] (boolean) Shows messages where ``text`` matches the recipients.
- [``sender``] (boolean) Shows messages where ``text`` matches the sender.
- [``subject``] (boolean) Shows messages where ``text`` matches the subject.
