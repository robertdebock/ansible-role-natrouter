# natrouter

Install and configure a NAT router on your system.

|Travis|GitHub|Quality|Downloads|
|------|------|-------|---------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-natrouter.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-natrouter)|[![github](https://github.com/robertdebock/ansible-role-natrouter/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-natrouter/actions)|[![quality](https://img.shields.io/ansible/quality/21915)](https://galaxy.ansible.com/robertdebock/natrouter)|[![downloads](https://img.shields.io/ansible/role/d/21915)](https://galaxy.ansible.com/robertdebock/natrouter)|

## Example Playbook

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.natrouter
```

The machine may need to be prepared using `molecule/resources/prepare.yml`:
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.sysctl
      sysctl_items:
        - name: net.ipv4.ip_forward
          value: 1
```

For verification `molecule/resources/verify.yml` run after the role has been applied.
```yaml
---
- name: Verify
  hosts: all
  become: yes
  gather_facts: yes

  tasks:
    - name: check if connection still works
      ping:
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## Role Variables

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for natrouter

# The network interface connected to the internet.
natrouter_public_interface: eth0

# The network address to translate.
natrouter_private_network: 192.168.1.0/24

# The destination.
natrouter_destination: 0.0.0.0/0

# The protocols to NAT.
natrouter_protocols:
  - tcp
  - udp
```

## Requirements

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.sysctl

```

## Context

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/natrouter.png "Dependency")

## Compatibility

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|alpine|all|
|el|7, 8|
|debian|buster, bullseye|
|fedora|31, 32|
|opensuse|all|
|ubuntu|focal, bionic, xenial|

The minimum version of Ansible required is 2.8 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.



## Testing

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-natrouter) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-natrouter/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `robertdebock`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `robertdebock`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `robertdebock`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

## License

Apache-2.0


## Author Information

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
