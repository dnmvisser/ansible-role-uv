# ansible-role-uv

Ansible role to install `uv` binaries through tarballs from
https://github.com/astral-sh/uv/releases.


# Role variables

| variable | description | default |
| -------- | ----------- | ------- |
| `uv_dir` | Directory where to put the binaries | `/usr/local/bin` |
| `uv_version` | Version to install | `latest`. This requires network connectivity to github.com every time |


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
