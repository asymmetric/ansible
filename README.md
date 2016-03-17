README
======

Ansible by default runs over SSH, and uses your `~/.ssh/config`.

For info on the recommended directory layout, see
[here](https://docs.ansible.com/ansible/playbooks_best_practices.html#directory-layout).

Main concepts
-------------

Ansible has 3 main concepts:

* playbooks
* inventories
* tasks

Also:

* roles
  * tasks
  * handlers
  * files

Tasks are what the name says, i.e. the things you want ansible to do on your
hosts.

Hosts are INI files where you assign hosts to groups. Here you would say
pbs-01/02 are part of the build groups.
You should create one inventory file per environment. This way, you can run the
same playbook on different environments by simply passing a different inventory
file.

Playbooks are where you connect hosts and tasks. This is where you say: run
these tasks on these hosts.

Tasks are grouped in roles. The "kermit" role has a "create deploy group" task.

A role is a collection of tasks, handlers (tasks which get triggered
by events) and files.  A playbook contains plays, which are where you map your
hosts to your roles.

Variables
---------

Ansible has a well-defined order of evaluation of variables.
Variables can be specified at the group level, at a host level, at a task level, etc.

If you want to define the IP address of a host, you normally do that in the
host's `host_vars` file (not in the inventory).

Variables which apply to a whole group can be set in a `group_vars` file.

Steps I took
------------

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
