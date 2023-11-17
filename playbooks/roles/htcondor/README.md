HTCondor Cluster Role
=========

[![License](https://img.shields.io/badge/license-Apache%202-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)

Ansible Role to install the HTCondor Software Suite (https://research.cs.wisc.edu/htcondor/) on a cluster using a member of the RedHat OS family.

Role Variables
--------------

Explicit variables that can be included in the playbook

```yaml
# HTCondor's semantic versioning syntax
# Major version values:
#   9
#   10
#   23
# Series (former name)
#   0   (stable)    - just bug fixes
#   x   (current)   - minor feature additions & bug fixes
major_version: 23
series: x

# the (DNS or IPv*) address of the central manager's host machine
cm_host_address: '192.168.122.13'

# The configuration flags for a nodes role in the pool
htcondor_role_manager: false
htcondor_role_access: false
htcondor_role_execute: false

# If the cluster uses a (networked) shared file system
shared_fs_domain: '192.168.22.42'
```

Also some import password variables stored in the (encrypted) `secrets.yml` file

```yaml
htcss_pool_password: changeme
ansible_become_password: pwd12345
```

Example Playbook
----------------

Here is an example (`cm.yml`) of a playbook to set up a node to be the HTCondor pool's central manager:

```yaml
- name: Set up the pool's central manager
  hosts: central_manager
  become: True

  vars:
    cm_host_address: '192.168.122.13'

  var_files:
    - secrets.yml

  roles: 
  - role: htcondor
    htcondor_role_manager: True
```

And here is how to run the above playbook:
```bash
ansible-playbook --ask-vault-pass cm.yml
```

This presumes that the inventory file `servers.yml` has been specified in `ansible.cfg` and has a subsection called `central_manager.`

