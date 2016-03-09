README
======

On CentOS, the OpenSSH is so old that some important features are not
supported. Therefore Ansible will use a Python implementation of OpenSSH called
**Paramiko**, which does not support everything though. [? what does it not support?]

Ansible by default runs over SSH, and uses your `~/.ssh/config`.

For info on the recommended directory layout, see [here](https://docs.ansible.com/ansible/playbooks_best_practices.html#directory-layout).

Main concepts
-------------

Ansible has 3 main concepts:

* playbooks
* inventories
* roles
* tasks
* handlers

Tasks are what the name says, i.e. the things you want ansible to do on your hosts.
A playbook contains plays, which are 

BLAH
----

* set `remote_user` to `vagrant` in `ansible.cfg`
* create one inventory file per environment
  * in that file, use hostnames
  * define IPs and other variables in `host_vars`
  * configure `ansible.cfg` to run `local.ini` by default
  * playbooks will reference groups, so they are orthogonal to the inventories

VAGRANT
-------

* define multiple machines
* assign them private IPs
* disable ssh key insertion (overkill)
* add insecure private key to ssh-agent `ssh-add ~/.vagrant.d/insecure_private_key`
  * so that you don't have to pass the file each time you invoke vagrant
