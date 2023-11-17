HTCondor Cluster Role
=========

[![License](https://img.shields.io/badge/license-Apache%202-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)

Ansible Role to install the HTCondor Software Suite (https://research.cs.wisc.edu/htcondor/) on a cluster using a member of the RedHat OS family.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Example Playbook
----------------

Here is an example (`cm.yml`) of a playbook to set up a node to be the HTCondor pool's central manager:

```yaml
- name: Set up the pool's central manager
  hosts: central_manager
  become: True

  vars:
    cm_host_address: '192.168.122.159'

  var_files:
    - secrets.yml

  roles: 
  - role: htcondor
    htcondor_role_manager: True
```

And here is how to run the above playbook:
```bash
ansible-playbook cm.yml -i ./inventory/servers.yml
```

