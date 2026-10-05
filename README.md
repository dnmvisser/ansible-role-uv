# ansible-role-uv

Ansible role to install uv


# Role variables

`uv_dir` - the directory where to put the binaries. Default: `/usr/local/bin`.
`uv_version` - the version to install. Default: `latest`. This requires network
connectivity to github.com.

# Example playbook

```yaml
---
- name: UV
  hosts: all
  become: true
  tasks:
    - name: Install uv
      ansible.builtin.import_role:
        name: ansible-role-uv
```
