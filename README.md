# roles/common/README.md

[![Build Status](https://travis-ci.org/cjsteel/common.svg?branch=master)](https://travis-ci.org/cjsteel/common)
[![Travis CI](http://img.shields.io/travis/csteel/common/default.svg?style=flat)](http://travis-ci.org/csteel/common/default)
[![Platforms](http://img.shields.io/badge/platforms-debian%20/%20ubuntu-lightgrey.svg?style=flat)](#)

## Description

common is an Ansible role used to  

- change default shell from dash to bash \
  - dash is set by default and need to change it to bash shell
- change umask default permission from 022 to 027
  - The default umask on Ubuntu is `022` which means that newly created files are readable by everyone, but only writable by the owner and group if USERGROUPS_ENAB: "yes" in /etc/login.defs
  - to better protect the directories and files, we will set the umask to remove **all** permissions for others and remove **write**  permission for groups.
  - afterwards, the permission of directory is 750 and the permission of file is 640. 
- others ...

## Recommended

Running Ansible in a virtual environment allows for a lot of testing flexibility.

* [docs/ansible-setup](docs/ansible-setup.md)

## Requirements

* Ansible

## Variables

### project_name/common.yml

* [example_playbook.yml](files/example_playbook.yml)

To install:

```shell
cd project_directory
cp roles/common/files/example_playbook.yml common.yml
# edit if required
nano common.yml
```

### project_name/site.yml

* [example_common.yml](files/example_site.yml)

From the projects main directory run the following:

```yaml
cp roles/common/files/example_playbook.yml common.yml
cat common.yml
```

### project/group_vars/all/project_defaults.yml

[files/group_vars/all/example_defaults.yml](files/group_vars/all/example_defaults.yml)

```yaml
cp roles/common/files/group_vars/all/example_defaults.yml group_vars/all/project_defaults.yml
cat group_vars/all/project_defaults.yml
```

### role variables

```sh
common_options:
  umask: "027"
  USERGROUPS_ENAB: "no"
```

## Ansible command to run

Move into the ace directory and run ansible-playbook

```sh
cd projects/ace
ansible-playbook -i inventory/dev systems.yml --limit "workstation" -u ansible
```



Move into the role directory and run vagrant:

```shell
cd roles/common
vagrant up
```

### Authors and license

- Robin Schneider | [e-mail](mailto:ypid@riseup.net)
- modified by [Andy Teng](http://mcin-cnim.ca/) | [e-mail](mailto:andy.teng@mcin.ca)
- [Christopher Steel](http://mcin-cnim.ca/) | [e-mail](mailto:christopher.steel@mcgill.ca)
- [John Le](http://mcin-cnim.ca/) | [e-mail](mailto:john.le@mcgill.ca)

License: [AGPLv3](https://tldrlegal.com/license/gnu-affero-general-public-license-v3-%28agpl-3.0%29)

***

