

Changes
=======

Changed with version 0.8.2:
---------------------------

- unified version numbering of the modules.
- ServiceError, ActionError and AuthorizationError are also importable from the package.
- some code cleanup.

Changes in the development process: .hgignore removed and .gitignore added, changes in setup.py, readme changed to restructured text.

As Atlassian has announced to drop support for mercurial on ``bitbucket`` und will remove the according repositories (in June 2020), development of fritzconnection has converted from ``hg`` to ``git`` and the repository has been transfered to ``github``. Unfortunately the issue- and discussion-history will be lost this way (even by keeping the new git-repository at bitbucket).


Changed with version 0.8.1:
---------------------------

FritzStatus: bugfix requiring a password in combination with fritzconnection >= 0.8.0

FritzStatus: added the ``external_ipv6`` attribute

FritzStatus: added the ``max_linked_bit_rate`` attribute for the physical rate. Also added the ``str_max_linked_bit_rate`` attribute for a more readable output. (password must be provided for these infomations)

FritzConnection: added the ``AuthorizationError`` exception.


Changed with version 0.8.0:
---------------------------

bugfix how servicenames are extracted from the xml-description files. However, the api has not changed.

The requirements are now fixed for lxml (4.3.4) and requests (2.22.0) as these versions are still supporting python 2.7


Changed with version 0.7.1 - 0.7.3:
-----------------------------------

bugfixes, no new features or other changes.


Changed with version 0.7.0:
---------------------------

FritzConnection does now check for the environment variables ``FRITZ_USER`` and ``FRITZ_PASSWORD`` in case that neither user nor password are given.

FritzStatus now accepts user and password as keyword-parameters. Keep in mind, that FritzBoxes may return different informations about the status depending whether these are gathered with or without a password.


Changed with version 0.6.5:
---------------------------

There is a new attribute *package_version*:

    >>> import fritzconnection
    >>> fritzconnection.package_version
    0.6.5

Because every module of the fritzconnection-package has it's own version, version-history of the package gets confusing over time. From now on every change of the content of the package is indicated by the the package-version. Every unchanged module keeps it's version. So i.e. the recent package-version is 0.6.5 but the fritzconnection-module is still in version 0.6 cause nothing has changed in this module since then.


Changed with version 0.6:
-------------------------

FritzConnection now uses long qualified names as ``servicename``, i.e. ``WLANConfiguration:1`` or ``WLANConfiguration:2``. So these servicenames can now be used to call actions on different services with the same name:

    >>> connection = FritzConnection()
    >>> info = connection.call_action('WANIPConnection:2', 'GetInfo')

For backward compatibility servicename-extensions like ':2' can be omitted on calling 'call_action'. In this case FritzConnection will use the extension ':1' as default.

On calling unknown services or actions in both cases KeyErrors has been raised. Calling an unknown service (or one unaccessible without a password) will now raise a ``ServiceError``. Calling an invalid action on a service will raise an ``ActionError``. Both Exceptions are Subclasses from the new ``FritzConnectionException``. The Exception classes can get imported from fritzconnection:

    >>> from fritzconnection import ServiceError, ActionError


