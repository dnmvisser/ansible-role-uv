# ansible-role-uv

Ansible role to install `uv` binaries through tarballs from
https://github.com/astral-sh/uv/releases.

## Role variables

| variable | type | description | default |
| -------- | ----------- | ------- | ---- |
| `uv_install` | `bool` |  Whether to install `uv` | `true` |
| `uv_dir` | `string` | Directory where to put the binaries | `/usr/local/bin` |
| `uv_version` | `string` | Version to install | `latest`. This requires network connectivity. Set this to a specific version to avoid this. |
| `uv_bin_path` | `string` | The path to the `uv` binary we should use | The `uv` in `uv_dir` if `uv_install` is true. Otherwise a relative path `uv`, which will pick one from your `$PATH` |
| `uv_venvs` | `list` of dicts  | List of virtualenvs that should be created. See below for the structure | `[]` (empty list, e.g. no virtualenvs) |

## Example playbook

```yaml
---
- name: UV
  hosts: all
  become: true
  tasks:
    - name: Install uv
      ansible.builtin.include_role:
        name: ansible-role-uv
      vars:
        uv_venvs:

          # Create venv and install packages
          - path: /opt/nagios1
            requirements: |
              pynag
              requests
              pysaml2
              docker
              boto3

          # Create venv and install/upgrade packages
          - path: /opt/nagios2
            state: upgraded
            requirements: |
              pynag
              requests
              pysaml2
              docker
              boto3

          # Create venv and sync requirements.
          # NOTE this will remove anything that is not listed in the requirements.
          - path: /opt/nagios3
            state: synced
            requirements: |
              certifi==2026.7.22
              cffi==2.1.1
              chardet==7.6.0
              charset-normalizer==3.5.2
              cryptography==50.0.2
              defusedxml==0.7.1
              elementpath==4.8.0
              idna==3.20
              pycparser==3.11
              pynag==1.1.2
              pyopenssl==26.4.0
              pysaml2==7.5.5
              python-dateutil==2.9.0.post0
              requests==2.34.2
              six==1.17.0
              urllib3==2.8.0
              xmlschema==2.5.1

          # Create venv and install packages, but using a custom/managed
          # python.
          - path: /opt/certbot
            requirements: |
              certbot
            environment:
              UV_PYTHON: 3.15
              UV_PYTHON_INSTALL_DIR: /usr/local/share/uv/python
              UV_PYTHON_PREFERENCE: managed
```
