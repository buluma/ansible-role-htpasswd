# [Ansible role htpasswd](#ansible-role-htpasswd)

htpasswd installation and helper role for Linux servers.

|GitHub|Issues|Pull Requests|Version|Downloads|
|------|------|-------------|-------|---------|
|[![github](https://github.com/buluma/ansible-role-htpasswd/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-htpasswd/actions/workflows/molecule.yml)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-htpasswd.svg)](https://github.com/buluma/ansible-role-htpasswd/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-htpasswd.svg)](https://github.com/buluma/ansible-role-htpasswd/pulls/)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-htpasswd.svg)](https://github.com/buluma/ansible-role-htpasswd/releases/)|[![Ansible Role](https://img.shields.io/ansible/role/d/buluma/htpasswd)](https://galaxy.ansible.com/ui/standalone/roles/buluma/htpasswd/documentation)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-htpasswd/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- become: true
  hosts: all
  name: Converge
  roles:
    - role: buluma.bootstrap
    - role: geerlingguy.apache
    - role: buluma.htpasswd
  vars:
    apache_remove_default_vhost: true
    apache_vhosts:
      - documentroot: /var/www/html
        extra_parameters:
          "<Directory \"/var/www/html\">\n    AuthType Basic\n    AuthName
          \"Apache with basic auth.\"\n    AuthUserFile /etc/httpd/passwdfile\n    Require
          valid-user\n</Directory>\n"
        listen: "80"
        servername: htpassword.test
    htpasswd_credentials:
      - group: apache
        mode: u+rw,g+r
        name: johndoe
        owner: root
        password: supersecure
        path: /etc/httpd/passwdfile
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-htpasswd/blob/master/molecule/default/prepare.yml):

```yaml
---
- hosts: all
  roles:
    - name: buluma.bootstrap
    - name: buluma.apache
    - name: buluma.nginx
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-htpasswd/blob/master/defaults/main.yml):

```yaml
---
htpasswd_credentials: []
htpasswd_nolog: true
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-htpasswd/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub |
|-------------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|
|[buluma.apache](https://galaxy.ansible.com/buluma/apache)|[![Build Status GitHub](https://github.com/buluma/ansible-role-apache/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-apache/actions)|
|[buluma.nginx](https://galaxy.ansible.com/buluma/nginx)|[![Build Status GitHub](https://github.com/buluma/ansible-role-nginx/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-nginx/actions)|

## [Context](#context)

This role is part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-htpasswd/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/r/robertdebock/enterpriselinux)|all|
|[Fedora](https://hub.docker.com/r/robertdebock/fedora)|all|
|[Debian](https://hub.docker.com/r/robertdebock/debian)|all|
|[Ubuntu](https://hub.docker.com/r/robertdebock/ubuntu)|all|

The minimum version of Ansible required is 2.9, tests have been done on:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them on [GitHub](https://github.com/buluma/ansible-role-htpasswd/issues).

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-htpasswd/blob/master/LICENSE).

## [Author Information](#author-information)

[Michael Buluma](https://buluma.github.io/)

### Get Help
- Report issues: https://github.com/buluma/ansible-role-htpasswd/issues/new
- See docs: https://docs.ansible.com/collection/gallery/ansible-role-htpasswd
