# Ansible Collection - karras.ocis

Ansible collection to manage ownCloud Infinite Scale (oCIS).

[![Test](https://github.com/karras/ansible-collection-ocis/actions/workflows/test.yml/badge.svg)](https://github.com/karras/ansible-collection-ocis/actions/workflows/test.yml) [![Release](https://github.com/karras/ansible-collection-ocis/actions/workflows/release.yml/badge.svg)](https://github.com/karras/ansible-collection-ocis/actions/workflows/release.yml)

## Compatibility

Currently only supports Arch Linux.

## Roles

The following roles are part of this collection:

| Role                       | Purpose                              | Dependencies |
| -------------------------- | ------------------------------------ | ------------ |
| [ocis](./roles/ocis)       | ownCloud Infinite Scale (oCIS) setup | n/a          |
| [traefik](./roles/traefik) | Traefik setup                        | n/a          |

Whenever possible only Ansible builtin modules are leveraged, which can lead to
some more complex tasks structures though.

## Usage

Follow the below steps to start using the collection:

* Install the latest collection version:

```sh
ansible-galaxy collection install karras.ocis
```

* Create a new playbook (e.g. `server.yml`) which includes the desired roles:

```yaml
---

- name: deploy and manage ocis
  hosts: all
  become: yes
  roles:
    - karras.ocis.ocis
    - karras.ocis.traefik
```

* Define an inventory, in this case Ansible is executed against localhost:

```ini
[dev]
ocis ansible_connection=local
```

* Finally run the playbook:

```sh
ansible-playbook server.yml -i inventory -K
```

## License

See [LICENSE](./LICENSE)
