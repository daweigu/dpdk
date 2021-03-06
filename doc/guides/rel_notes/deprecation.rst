ABI and API Deprecation
=======================

See the :doc:`guidelines document for details of the ABI policy </contributing/versioning>`.
API and ABI deprecation notices are to be posted here.


Deprecation Notices
-------------------

* eal: DPDK runtime configuration file (located at
  ``/var/run/.<prefix>_config``) will be moved. The new path will be as follows:

  - if DPDK is running as root, path will be set to
    ``/var/run/dpdk/<prefix>/config``
  - if DPDK is not running as root and $XDG_RUNTIME_DIR is set, path will be set
    to ``$XDG_RUNTIME_DIR/dpdk/<prefix>/config``
  - if DPDK is not running as root and $XDG_RUNTIME_DIR is not set, path will be
    set to ``/tmp/dpdk/<prefix>/config``

* eal: both declaring and identifying devices will be streamlined in v18.08.
  New functions will appear to query a specific port from buses, classes of
  device and device drivers. Device declaration will be made coherent with the
  new scheme of device identification.
  As such, ``rte_devargs`` device representation will change.

  - The enum ``rte_devtype`` was used to identify a bus and will disappear.
  - Functions previously deprecated will change or disappear:

    + ``rte_eal_devargs_type_count``
    + ``rte_eal_devargs_parse`` will change its format and use.

* pci: Several exposed functions are misnamed.
  The following functions are deprecated starting from v17.11 and are replaced:

  - ``eal_parse_pci_BDF`` replaced by ``rte_pci_addr_parse``
  - ``eal_parse_pci_DomBDF`` replaced by ``rte_pci_addr_parse``
  - ``rte_eal_compare_pci_addr`` replaced by ``rte_pci_addr_cmp``

* eal: a new set of mbuf mempool ops name APIs for user, platform and best
  mempool names have been defined in ``rte_mbuf`` in v18.02. The uses of
  ``rte_eal_mbuf_default_mempool_ops`` shall be replaced by
  ``rte_mbuf_best_mempool_ops``.
  The following function is deprecated since 18.05, and will be removed
  in 18.08:

  - ``rte_eal_mbuf_default_mempool_ops``

* mbuf: The opaque ``mbuf->hash.sched`` field will be updated to support generic
  definition in line with the ethdev TM and MTR APIs. Currently, this field
  is defined in librte_sched in a non-generic way. The new generic format
  will contain: queue ID, traffic class, color. Field size will not change.

* mbuf: the macro ``RTE_MBUF_INDIRECT()`` will be removed in v18.08 or later and
  replaced with ``RTE_MBUF_CLONED()`` which is already added in v18.05. As
  ``EXT_ATTACHED_MBUF`` is newly introduced in v18.05, ``RTE_MBUF_INDIRECT()``
  can no longer be mutually exclusive with ``RTE_MBUF_DIRECT()`` if the new
  experimental API ``rte_pktmbuf_attach_extbuf()`` is used. Removal of the macro
  is to fix this semantic inconsistency.

* ethdev: In v18.11 ``DEV_RX_OFFLOAD_CRC_STRIP`` offload flag will be removed, default
  behavior without any flag will be changed to CRC strip.
  To keep CRC ``DEV_RX_OFFLOAD_KEEP_CRC`` flag is required.
  ``KEEP_CRC``: Keep CRC in packet
  No flag: Strip CRC from packet

* ethdev: the legacy filter API, including
  ``rte_eth_dev_filter_supported()``, ``rte_eth_dev_filter_ctrl()`` as well
  as filter types MACVLAN, ETHERTYPE, FLEXIBLE, SYN, NTUPLE, TUNNEL, FDIR,
  HASH and L2_TUNNEL, is superseded by the generic flow API (rte_flow) in
  PMDs that implement the latter.
  Target release for removal of the legacy API will be defined once most
  PMDs have switched to rte_flow.

* pdump: As we changed to use generic IPC, some changes in APIs and structure
  are expected in subsequent release.

  - ``rte_pdump_set_socket_dir`` will be removed;
  - The parameter, ``path``, of ``rte_pdump_init`` will be removed;
  - The enum ``rte_pdump_socktype`` will be removed.
