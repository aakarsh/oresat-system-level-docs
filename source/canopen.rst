CANopen
=======

A CAN bus is used as the main data and control bus for cards on OreSat. All
cards use the CANopen protocol and the C3 is network manager.

.. note:: New to CANopen? CANopen is specification are definited by CAN in
   Automation (CiA). Checkout `CiA CANopen`_ for the specifications. Also
   checkout `Wikipedia CANopen page`_ for a overview.

All OreSat node will also follow `ECSS CANbus Existion Protocal`_ as it
extends CANopen for space systems.

Node ID and Extra TPDOs
-----------------------

Normally all CANopen nodes have 4 TPDO (Transmit PDOs) and since all TPDO are 8
bytes long  there is only 64 bytes available for TPDOs for a node. This is
not enought for most OreSat nodes. To give OreSat nodes more bytes for TPDOs,
every OreSat node takes the place of 4 nodes, so every OreSat node can have 16
TPDO, therefor 128 bytes available for TPDOs.

Example: A card with node ID 0x20 can also use all TPDOs for 0x21, 0x22, & 0x23
as no node on OreSat will ever use those 3 node IDs.

.. note:: Node 0x00 is not valid node ID, so node 0x01 (the C3 card) will only
   have 12 TPDOs.

.. note:: Nodes with a node id >= 0x7C are consider unknown nodes (their node
   ID are not set, so it default to >= 0x7C).

Valid node IDs on OreSat are:

.. code-block:: bash

   0x01 0x04 0x08 0x0C 0x10 0x14 0x18 0x1C 0x20 0x24 0x28 0x2C 0x30 0x34 0x38
   0x3C 0x40 0x44 0x48 0x4C 0x50 0x54 0x58 0x5C 0x60 0x64 0x68 0x6C 0x70 0x74
   0x78

Time on CAN bus
---------------

On OreSat SCET (SpaceCraft Elapics Time) is used for time  and the UNIX
epoch (00:00:00 UTC on 1 January 1970) is used the epoch.

SCET is define as:

.. code-block:: c

  struct {
      unsigned 32 Coarse Time
      unsigned 24 Fine Time (sub seconds)
  } SCET

Time Sync TPDO
--------------

The C3's TPDO1 (COB-ID 0x181) is used for time syncing on OreSat. It will
contain the current SCET. Any cards that care about time (mostly C3
and Linux boards) will have a RPDO configure for that Time Sync TPDO and set
the card's local time to the time in the TPDO immediately.

The C3 and GPS cards can both send the Time Sync TPDO. The C3 has a RTC and the
GPS card get the a timestamp in the GPS message. The C3 can just send Time
Sync TPDO as needed. If the GPS card is on and has locked on to 4+ GPS,
satellites it will set it own local clock, then the C3 can send a SYNC message
and the GPS card will responed with the Time Sync TPDO allowing the C3 and
other cards to sync their time to the GPS time.

.. _Wikipedia CANopen page: https://en.wikipedia.org/wiki/CANopen
.. _CiA CANopen: https://www.can-cia.org/canopen
.. _ECSS CANbus Existion Protocal: https://ecss.nl/standard/ecss-e-st-50-15c-space-engineering-canbus-extension-protocol-1-may-2015/
