natrouter
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-natrouter.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-natrouter)

Provides an easy way to setup a nat router.

Context
--------
This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/natrouter.png "Dependency")

Requirements
------------

A machine with 2 (or more) interfaces.
Access to a repository containing packages, likely on the internet.
Have iptables installed. Hint: robertdebock.iptables

Role Variables
--------------

- natrouter_public_interface - The interface to go out over, defaults to eth0.
- natrouter_private_network - The CIDR notation of the network where traffic will come from, defaults to 192.168.1.0/24.
- natrouter_destination - The destination to translate, defaults to 0.0.0.0/0.
- natrouter_protocols: - The protcols to use, defaults to udp and tcp.

Dependencies
------------

These dependencies are not "hard", but rather "loose".

- [robertdebock.bootstrap](https://travis-ci.org/robertdebock/ansible-role-bootstrap)
- [robertdebock.iptables](https://travis-ci.org/robertdebock/ansible-role-iptables)

Download the dependencies by issuing this command:
```
ansible-galaxy install --role-file requirements.yml
```

Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.3|ansible 2.4|ansible 2.5|
|------------|-----------|-----------|-----------|
|alpine-latest|yes|yes|yes|
|alpine-edge|yes|yes|yes|
|archlinux|yes|yes|yes|
|centos-6|yes|yes|yes|
|centos-latest|yes|yes|yes|
|debian-stable|yes|yes|yes|
|debian-latest|yes|yes|yes|
|debian-wheezy|yes|yes|yes|
|fedora-latest|yes|yes|yes|
|fedora-rawhide|yes|yes|yes|
|opensuse-leap|yes|yes|yes|
|opensuse-tumbleweed|yes|yes|yes|
|ubuntu-artful|yes|yes|yes|
|ubuntu-latest|yes|yes|yes|

Example Playbook
----------------

```
- hosts: servers

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.iptables
    - role: robertdebock.natrouter
      public_interface: enp0s3
      private_network: 172.16.0.0/24
```

Install this role using `galaxy install robertdebock.natrouter`.

License
-------

Apache License, Version 2.0

Author Information
------------------

Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
