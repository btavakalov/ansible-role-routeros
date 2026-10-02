# Ansible role: routeros

Declarative configuration of MikroTik RouterOS devices over the API, on top of
[`community.routeros`](https://galaxy.ansible.com/ui/repo/published/community/routeros/).
One variable per RouterOS menu path; `null` (the default) leaves a path alone,
otherwise the variable is the full desired contents of that path. See
`defaults/main/` for the list.

```bash
ansible-galaxy collection install -r requirements.yaml
```

```yaml
- name: Configure RouterOS
  hosts: routeros          # ansible_connection: local, API credentials in group_vars
  gather_facts: false
  roles:
    - routeros
```

`--tags info` prints model and version, `--tags state` writes a sanitized
configuration snapshot. `--check --diff` is supported throughout.
