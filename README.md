# [Ansible role htpasswd](#ansible-role-htpasswd)

htpasswd installation and helper role for Linux servers.

|GitHub|GitLab|Downloads|Version|
|------|------|---------|-------|
|[![github](https://github.com/buluma/ansible-role-htpasswd/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-htpasswd/actions)|[![gitlab](https://gitlab.com/shadowwalker/ansible-role-htpasswd/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-htpasswd)|[![downloads](https://img.shields.io/ansible/role/d/buluma/htpasswd)](https://galaxy.ansible.com/buluma/htpasswd)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-htpasswd.svg)](https://github.com/buluma/ansible-role-htpasswd/releases/)|

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
          extra_parameters: "<Directory \"/var/www/html\">\n    AuthType Basic\n \
            \   AuthName \"Apache with basic auth.\"\n    AuthUserFile /etc/httpd/passwdfile\n\
            \    Require valid-user\n</Directory>\n"
          listen: '80'
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

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-bootstrap)|
|[bukuma.apache](https://galaxy.ansible.com/buluma/bukuma.apache)|[![Build Status GitHub](https://github.com/buluma/bukuma.apache/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/bukuma.apache/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/bukuma.apache/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/bukuma.apache)|
|[buluma.nginx](https://galaxy.ansible.com/buluma/nginx)|[![Build Status GitHub](https://github.com/buluma/ansible-role-nginx/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-nginx/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-nginx/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-nginx)|

## [Context](#context)

This role is part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-htpasswd/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/r/buluma/enterpriselinux)|all|
|[Fedora](https://hub.docker.com/r/buluma/fedora)|all|
|[Debian](https://hub.docker.com/r/buluma/debian)|all|
|[Ubuntu](https://hub.docker.com/r/buluma/ubuntu)|all|

The minimum version of Ansible required is 2.9, tests have been done on:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them on [GitHub](https://github.com/buluma/ansible-role-htpasswd/issues).

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-htpasswd/blob/master/LICENSE).

## [Author Information](#author-information)

[Michael Buluma](https://buluma.github.io/)

