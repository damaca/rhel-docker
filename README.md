ansible-rhel-docker
============

Ansible role to deploy docker on a plain RHEL OS. It supports 2 different OS versions: RHEL-6 and RHEL-7.

Requirements
------------

This role is only available for RedHat-based systems.

This role requires to disable SELinux in order to manage groups before using the role. For example:

```yaml
- name: Disable SELinux
  hosts: all
  sudo: true
  tasks:
    - selinux: policy=targeted state=permissive

- name: Install basic software
  hosts: servers
  roles:
    - role: ansible-rhel

- name: Enable SELinux
  hosts: all
  tasks:
    - selinux: policy=targeted state=enforcing
```

Role Variables
--------------

* **docker_version** (Optional). Docker version. It is possible to use `latest` to install the latest version, or a specific version (e.g. 1.10.3). By default, the docker runtime is not installed.
* **dockerpy_version** (Optional). Docker-py module version. You may want to use a specific version of the docker-py module in order to avoid a [bug](https://github.com/ansible/ansible/issues/17495) that affects ansible versions < `2.2` . This variable only affects the Docker installation, so you should use it together with the **docker_version** variable. By default, when using the docker_version variable and omitting dockerpy_version, the latest version of the docker-py library is installed.
