# [htpasswd](#htpasswd)

htpasswd installation and helper role for Linux servers.

|GitHub|GitLab|Quality|Downloads|Version|Issues|Pull Requests|
|------|------|-------|---------|-------|------|-------------|
|[![github](https://github.com/buluma/ansible-role-htpasswd/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-htpasswd/actions)|[![gitlab](https://gitlab.com/buluma/ansible-role-htpasswd/badges/master/pipeline.svg)](https://gitlab.com/buluma/ansible-role-htpasswd)|[![quality](https://img.shields.io/ansible/quality/)](https://galaxy.ansible.com/buluma/htpasswd)|[![downloads](https://img.shields.io/ansible/role/d/)](https://galaxy.ansible.com/buluma/htpasswd)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-htpasswd.svg)](https://github.com/buluma/ansible-role-htpasswd/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-htpasswd.svg)](https://github.com/buluma/ansible-role-htpasswd/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-htpasswd.svg)](https://github.com/buluma/ansible-role-htpasswd/pulls/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
```yaml
---
# Note: This playbook is built to work on Red Hat-derivative Linux OSes.
- name: Converge
  hosts: all
  become: true

  vars:
    htpasswd_credentials:
      - path: /etc/httpd/passwdfile
        name: johndoe
        password: 'supersecure'
        owner: root
        group: apache
        mode: 'u+rw,g+r'

    apache_remove_default_vhost: true
    apache_vhosts:
      - listen: "80"
        servername: "htpassword.test"
        documentroot: "/var/www/html"
        extra_parameters: |
              <Directory "/var/www/html">
                  AuthType Basic
                  AuthName "Apache with basic auth."
                  AuthUserFile /etc/httpd/passwdfile
                  Require valid-user
              </Directory>

  roles:
    - role: buluma.bootstrap
    - role: buluma.apache
    - role: buluma.htpasswd
```


## [Role Variables](#role-variables)

The default values for the variables are set in `defaults/main.yml`:
```yaml
---
# Define this variable if you'd like to override the defaults.
# htpasswd_required_packages: []

# Whether to show htpasswd credentials in Ansible's log output.
htpasswd_nolog: true

# A list of htpasswd credentials.
htpasswd_credentials: []
# - path: /etc/nginx/passwdfile
#   name: johndoe
#   password: 'supersecure'
#   owner: root
#   group: www-data
#   mode: 0640

# - path: /etc/apache2/passwdfile
#   name: janedoe
#   password: 'supersecure'
#   owner: root
#   group: www-data
#   mode: 0640
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-htpasswd/blob/main/requirements.txt).


## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.co.ke/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-htpasswd/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|el|7, 8|
|fedora|all|
|debian|all|
|ubuntu|all|

The minimum version of Ansible required is 2.9, tests have been done to:

- The previous version.
- The current version.
- The development version.



If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-htpasswd/issues)

## [License](#license)

Apache-2.0

## [Author Information](#author-information)

[Michael Buluma](https://buluma.github.io/)
