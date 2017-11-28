ansible-role-natrouter
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-natrouter.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-natrouter)

Provides an easy way to setup a nat router.

Requirements
------------

A machine with 2 (or more) interfaces.
Access to a repository containing packages, likely on the internet.

Role Variables
--------------

- public_interface - The interface to go out over, defaults to eth0
- private_network - The CIDR notation of the network where traffic will come from, default to 192.168.1.0/24

Dependencies
------------

- robertdebock.ansible-role-iptables

Download the dependencies by issuing this command:
```
ansible-galaxy install --role-file requirements.yml
```

Example Playbook
----------------

```
- hosts: servers

  roles:
    - role: robertdebock.ansible-role-natrouter
      public_interface: enp0s3
      private_network: 172.16.0.0/24
```

Install this role using `galaxy install robertdebock.ansible-role-natrouter`.

License
-------

Apache License, Version 2.0

Author Information
------------------

Robert de Bock <robert@meinit.nl>
