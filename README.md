Firewalld
=========

firewalld can be used to manage firewall confoguration on a linux vm.
This role configures the firewalld configuration for using PostgreSQL, etcd, stolon-proxy, etc.
This role is part of PgVillage, which is an opinated PostgreSQL deployment for Virtual Machines.

Requirements
------------

This role aims at using an RPM from the MannemSolutions repo.

Role Variables
--------------

Please see the [API documentation](docs/api.md) for a description of all variables.
Defaults are defined in [defaults/main.yml](defaults/main.yml).


Dependencies
------------

No dependencies


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - pgvillage.firewalld

License
-------

PostgreSQL

Author Information
------------------

PgVillage is an Open Community.
Main contributor is Nibble-IT.
