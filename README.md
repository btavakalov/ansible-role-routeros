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
configuration snapshot, `--tags export` saves `/export` output read over SSH
(see `routeros_user_ssh_keys`). `--check --diff` is supported throughout.

`tasks_from: upgrade` installs a newer RouterOS from the configured update channel
and then upgrades the routerboard firmware, waiting for each reboot. Run it from a
play with `serial: 1`, so that routers reboot one at a time; `--check` only shows
the versions.

```yaml
- name: Upgrade RouterOS
  hosts: routeros
  gather_facts: false
  serial: 1
  tasks:
    - name: Upgrade
      ansible.builtin.include_role:
        name: routeros
        tasks_from: upgrade
```
