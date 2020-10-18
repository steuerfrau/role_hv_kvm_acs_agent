role_hv_kvm_acs_agent
=========

Installs the CloudStack Agent on top of a default KVM hypervisor setup.

Requirements
------------

playbook_baseinstall

Role Variables
--------------

```
cat defaults/main.yml 
---
# defaults file for role_hv_kvm_acs_agent
role_hv_kvm_acs_agent_acs_version: 4.14
```
Can be overwritten.

Dependencies
------------

```
- name: Create Repositories
  import_role:
    name: role_mod_repositories
  vars:
    - role_mod_repositories_yum_repos:
        - name: CloudStack-ShapeBlue
          description: "ShapeBlue CloudStack Repository."
          file: "CloudStack-ShapeBlue"
          baseurl: "http://packages.shapeblue.com/cloudstack/upstream/centos7/{{ role_hv_kvm_acs_agent_acs_version }}"
          gpgcheck: "yes"
          gpgkey: "http://packages.shapeblue.com/release.asc"
          enabled: "yes"

- name: Install KVM Hypervisor
  import_role:
    name: role_hv_kvm

- name: Set SELinux to permissive
  import_role:
    name: role_bi_selinux
  vars:
    - role_bi_selinux_selinux_mode: "permissive"
```

Example Playbook
----------------

Used from playbook_acs_single_node.

License
-------

GNU Public License v3.0

Author Information
------------------

Melanie Desaive, m.desaive@mailbox.org
