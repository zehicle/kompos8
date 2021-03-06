Kubernetes install for Digital Rebar
==================================== 

Please see http://rebar.digital for details.

Status
------

This is a work in progress... it will replace the RackN Kubernetes workload.


Objective
---------

Decompose Kubernetes installation into composable units so that each role is stand alone.  For now, we are using Ansible primarily to perform functions, but individual roles could be replaced with other DSLs or even directly with bash instructions.

The goal of the decomposition is to isolate individual services as much as possible.  Variables passed into each role should be specific to those needed for that function.

Defaults: see group_vars/all.yml

Design Decisions
----------------

The following items are recognized as principles for the Kompos8 scripts:

  1. To streamline development, Kompos8 will require SystemD.
  #. Further, we will not (re)package the simple Kubernetes GO services into containers.
  #. For Ansible, we will avoid using unneeded variables and default() in the plays.  We would rather have them fail quickly when information is missing.
  #. While we want create portable playbooks without Rebar dependencies, we are NOT trying to create playbooks that stand alone without Rebar.

Architecture Requirements
-------------------------

  1. Do not comingle services but allow them to co-exist
  #. Must be multi-node

Naming & Conventions
--------------------

Kompos8 is a play on "composate" with the K (for Kubernetes or k8s) substituted for C and 8 (for 8 in k8s) substituted for ate.  The idea is to have a composable install.

Variables in the workload should be nested and generally follow:

  * k8s. for kubernetes items with additional grouping
  * cluster. for cluster items
  * provider. for provider (e.g. cloud) items
  * rebar. for rebar specific items
  * user. for Kubernetes user items (account is the service account)

Enable to ``debug`` variable to see specifics in the runs.

