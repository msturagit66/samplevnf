.. This work is licensed under a Creative Commons Attribution 4.0 International
.. License.
.. http://creativecommons.org/licenses/by/4.0
.. (c) OPNFV, Intel Corporation and others.


OPNFV Jerma Release
===================
* The only supported test VNF in this release for dataplane benchmarking purposes is PROX
* PROX supporting up to DPDK:20.05
* Introducing ability to make test cloud-configured dataplane networking benchmarks using
  ETSI NFV TST009 standard methods
* Test automation using X-testing


OPNFV Hunter Release
====================

This Hunter release provides *SampleVNF* as a approx VNF repository for
VNF/NFVI testing, characterization and OPNFV feature testing, automated on
OPNFV platform, including:

* Documentation generated with Sphinx

  * User Guide

  * Developer Guide

  * Release notes (this document)

  * Results

* Automated SampleVNF test suit in OPNFV Yardstick Project

* SampleVNF source code

For Hunter release, the *SampleVNF* supported:

+----------------+---------------------------------------------------------+-------------------+
| *VNF*          |                 *Name*                                  |    *version*      |
+----------------+---------------------------------------------------------+-------------------+
| *CGNAPT*       | Carrier Grade Network Address and port Translation .5.0 |     v0.1.0        |
+----------------+---------------------------------------------------------+-------------------+
| *Prox*         | Packet pROcessing eXecution engine                      |     v0.40.0       |
|                | acts as traffic generator, L3FWD, L2FWD, BNG etc        |                   |
+----------------+---------------------------------------------------------+-------------------+
| *vACL*         | Access Control List                                     |     v0.1.0        |
+----------------+---------------------------------------------------------+-------------------+
| *vFW*          | Firewall                                                |     v0.1.0        |
+----------------+---------------------------------------------------------+-------------------+
| *UDP_replay*   | UDP_Replay                                              |     v0.1.0        |
+----------------+---------------------------------------------------------+-------------------+

.. note:: Highlevel Desgin and features supported by each of the VNFs is described in Developer
          and user guide.

For Hunter release, the *SampleVNF* is used for the following
testing:

* OPNFV platform testing - generic test cases to measure the categories:

  * NFVI Characterization:

    * Network

  * VNF Characterization:

    * Network - rfc2544, rfc3511, latency, http_test etc


The *SampleVNF* is developed in the OPNFV community, by the SampleVNF team.
The *Network Service Benchmarking* SampleVNF Characterization Testing tool is a part of the
Yardstick Project.

.. note:: The test case description template used for the SampleVNF in yardstick
  test cases is based on the document `ETSI GS NFV-TST 001`_; the results report template
  used for the SampleVNF test results is based on the IEEE Std 829-2008.

.. _ETSI GS NFV-TST 001: https://portal.etsi.org/webapp/workprogram/Report_WorkItem.asp?WKI_ID=46009


Release Data
------------

+--------------------------------------+--------------------------------------+
| **Project**                          | SampleVNF                            |
|                                      |                                      |
+--------------------------------------+--------------------------------------+
| **Repo/tag**                         | opnfv-8.0                            |
|                                      |                                      |
+--------------------------------------+--------------------------------------+
| **SampleVNF Docker image tag**       | Hunter 8.0                           |
|                                      |                                      |
+--------------------------------------+--------------------------------------+
| **Release designation**              | Hunter 8.0                           |
|                                      |                                      |
+--------------------------------------+--------------------------------------+
| **Release date**                     | "May 10 2019"                        |
|                                      |                                      |
+--------------------------------------+--------------------------------------+
| **Purpose of the delivery**          | Hunter alignment to Released         |
|                                      | bug-fixes for the following:         |
|                                      |                                      |
|                                      | - Memory leak                        |
|                                      | - minimum latency                    |
|                                      | - Increase default mbuf size and     |
|                                      |   code simplification/cleanup        |
|                                      | - Crash in rx/tx distribution        |
|                                      |                                      |
+--------------------------------------+--------------------------------------+


Deliverables
------------

Documents
^^^^^^^^^

 - User Guide: http://artifacts.opnfv.org/samplevnf/docs/testing_user_userguide/index.html

 - Developer Guide: http://artifacts.opnfv.org/samplevnf/docs/testing_developer/index.html


Software Deliverables
^^^^^^^^^^^^^^^^^^^^^

 - The SampleVNF Docker image: To be added


**SampleVNF tested on Contexts**

+---------------------+-------------------------------------------------------+
| **Context**         | **Description**                                       |
|                     |                                                       |
+---------------------+-------------------------------------------------------+
| *Heat*              | Models orchestration using OpenStack Heat             |
|                     |                                                       |
+---------------------+-------------------------------------------------------+
| *Node*              | Models Baremetal, Controller, Compute                 |
|                     |                                                       |
+---------------------+-------------------------------------------------------+
| *Standalone*        | Models VM running on Non-Managed NFVi                 |
|                     |                                                       |
+---------------------+-------------------------------------------------------+

Document Version Changes
^^^^^^^^^^^^^^^^^^^^^^^^

This is the first version of the SampleVNF  in OPNFV.
It includes the following documentation updates:

- SampleVNF User Guide:

- SampleVNF Developer Guide

- SampleVNF Release Notes for SampleVNF: this document


Feature additions
^^^^^^^^^^^^^^^^^

- Support for DPDK 18.05 and DPDK 18.08
- Add support for counting non dataplane related packets
- test improvements and fixes for image creation
- Local Documentation Builds
- Improve l3fwd performance
- Enable the local cache mac address
- Initial support for DPDK 18.05
- Adding centos.json to be used with packer to generate a VM with PROX
- Adding support for Ubuntu 17.10...
- Get multiple port stats simultaneously
- Increase default mbuf size and code simplification/cleanup
- update from src port in the pvt/pub handler

Bug fixes:
- Fix potential crash with latency accuracy
- TempFix: vCGNAPT/vACL ipv4 perf issue
- Temp Fix for vFW perf issue
- fix code standard in VNFs/DPPD-PROX/handle_esp.c
- Workaround DPDK net/virtio queue setup issue
- Fix potential crash when shuffling mbufs


Known Issues/Faults
^^^^^^^^^^^^^^^^^^^
- Huge page freeing needs to be handled properly while running the application else it might
  cause system crash. Known issue from DPDK.
- UDP Replay is used to capture throughput for dynamic cgnapt
- Hardware Checksum offload is not supported for IPv6 traffic
- SampleVNF on sriov is tested till 4 threads
- Rest API is supported only for vACL, vFW, vCGNAPT
- Rest API uses port 80, make sure other webservices are stopped before using SampleVNF RestAPI.

Corrected Faults
^^^^^^^^^^^^^^^^

Hunter 8.2:

+----------------------------+----------------------------------------------------------------------+
| **JIRA REFERENCE**         | **DESCRIPTION**                                                      |
+----------------------------+----------------------------------------------------------------------+
| SAMPLEVNF-129              |  Support for DPDK 18.05 and DPDK 18.08                               |
+----------------------------+----------------------------------------------------------------------+
| SAMPLEVNF-130              |  Add support for counting non dataplane related packets              |
+----------------------------+----------------------------------------------------------------------+
| SAMPLEVNF-131              |  test improvements and fixes for image creation                      |
+----------------------------+----------------------------------------------------------------------+
| SAMPLEVNF-132              |  Local Documentation Builds                                          |
+----------------------------+----------------------------------------------------------------------+
| SAMPLEVNF-133              |  Improve l3fwd performance                                           |
+----------------------------+----------------------------------------------------------------------+
| SAMPLEVNF-134              |  Enable the local cache mac address                                  |
+----------------------------+----------------------------------------------------------------------+
| SAMPLEVNF-135              |  Initial support for DPDK 18.05                                      |
+----------------------------+----------------------------------------------------------------------+
| SAMPLEVNF-136              |  Adding centos.json to be used with packer to generate a VM with PROX|
+----------------------------+----------------------------------------------------------------------+
| SAMPLEVNF-137              |  Adding support for Ubuntu 17.20...                                  |
+----------------------------+----------------------------------------------------------------------+
| SAMPLEVNF-138              |  Get multiple port stats simultaneously                              |
+----------------------------+----------------------------------------------------------------------+
| SAMPLEVNF-139              |  Increase default mbuf size and code simplification/cleanup          |
+----------------------------+----------------------------------------------------------------------+
| SAMPLEVNF-140              |  update from src port in the pvt/pub handler                         |
+----------------------------+----------------------------------------------------------------------+




Bug Fix Jira:

+----------------------------+-------------------------------------------------------------------+
| **JIRA REFERENCE**         | **DESCRIPTION**                                                   |
+----------------------------+-------------------------------------------------------------------+
| SAMPLEVNF-141              |  Fix potential crash with latency accuracy                        |
+----------------------------+-------------------------------------------------------------------+
| SAMPLEVNF-142              |  TempFix: vCGNAPT/vACL ipv4 perf issue                            |
+----------------------------+-------------------------------------------------------------------+
| SAMPLEVNF-143              |  Temp Fix for vFW perf issue                                      |
+----------------------------+-------------------------------------------------------------------+
| SAMPLEVNF-144              |  fix code standard in VNFs/DPPD-PROX/handle_esp.c                 |
+----------------------------+-------------------------------------------------------------------+
| SAMPLEVNF-145              |  Workaround DPDK net/virtio queue setup issue                     |
+----------------------------+-------------------------------------------------------------------+
| SAMPLEVNF-146              |  Fix potential crash when shuffling mbufs                         |
+----------------------------+-------------------------------------------------------------------+

Hunter known restrictions/issues
--------------------------------
+-----------+-----------+----------------------------------------------+
| Installer | Scenario  |  Issue                                       |
+===========+===========+==============================================+
|           |           |                                              |
+-----------+-----------+----------------------------------------------+


Open JIRA tickets
-----------------

+----------------------------+------------------------------------------------+
| **JIRA REFERENCE**         | **DESCRIPTION**                                |
|                            |                                                |
+----------------------------+------------------------------------------------+
|                            |                                                |
|                            |                                                |
+----------------------------+------------------------------------------------+


Useful links
------------

 - wiki project page: https://wiki-old.opnfv.org/display/SAM

 - wiki SampleVNF Hunter release planing page: https://wiki.opnfv.org/display/SAM/G+-+Release+SampleVNF+planning

 - SampleVNF repo: https://git.opnfv.org/samplevnf/

 - SampleVNF IRC chanel: #opnfv-samplevnf
