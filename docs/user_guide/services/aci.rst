ACI
===

This section lists the services which are supported on Application Centric Infrastructure (ACI).

  * `execute <#execute>`__
  * `configure <#configure>`__
  * `reload <#reload>`__

The ACI plugin supports only APIC and N9K (in ACI mode) using the `series` option. Specify ``aci``
as `os` option and ``apic`` or ``n9k`` as the `series` option.

.. note::

    The ``connect`` service for ACI plugin supports detection of the `setup` state of the APIC and
    `boot` state of the N9K switches in ACI mode.  If the `connect()` service finds the devices in
    `setup` or `boot` state, it is up to the user to handle the transition to the `enable` state.


The following generic services are also avaiable:

  * `send`_
  * `sendline`_
  * `expect`_

.. _send: generic_services.html#send
.. _sendline: generic_services.html#sendline
.. _expect: generic_services.html#expect


execute
-------

This service is used to execute arbitrary commands on the device. Though it is
intended to execute non-interactive commands. In case you wanted to execute
interactive command use `reply` option.


===============   ======================    ========================================
Argument          Type                      Description
===============   ======================    ========================================
timeout           int (default 60 sec)      timeout value for the overall interaction.
reply             Dialog                    additional dialog
command           str                       command to execute
===============   ======================    ========================================

`Execute` service returns the output of the command in the string format
or it raises an exception. You can expect a SubCommandFailure
error in case anything goes wrong.



configure
---------

This service is supported for APIC only, not for N9K devices in ACI mode.

For more info, see `configure`_

.. _configure: generic_services.html#configure


reload
------

The reload service is supported for both APIC and N9K devices.

=================   ======================    ===========================================================
Argument            Type                      Description
=================   ======================    ===========================================================
reload_command      str                       (optional) Command to reload the device
dialog              Dialog                    (optional) Additional dialogs to use
timeout             int (default 60 sec)      (optional) reload timeout
discovery_timeout   int (default 0 sec)       (optional) Time to wait for discovery complete after reload
=================   ======================    ===========================================================

The default reload command for ACPI is `acidiag reboot`,
the default reload command for N9K is `reload`.

The `discovery_timeout` is only supported for N9K devices.
