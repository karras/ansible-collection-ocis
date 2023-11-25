# Ansible Role - ocis

Manages and deploys ownCloud Infinite Scale (oCIS).

**Note:** Make sure to read and agree to the [oCIS
EULA](https://doc.owncloud.com/ocis/next/#end-user-license-agreement-eula)
first.

## Example Playbook

As this role is tested via Molecule one can use [that
playbook](./molecule/default/converge.yml) as a starting point:

```yaml
---

- name: Converge
  hosts: all
  gather_facts: true

  roles:
    - role: ocis
```

## Role Variables

The default variables are defined in [defaults/main.yml](./defaults/main.yml):

```yaml
# Directory where to place the oCIS binary
ocis_bin_path: /usr/local/bin

# Directory where to place the oCIS configs
ocis_config_path: /etc/ocis

# Directory where to place the oCIS data
ocis_data_path: /var/lib/ocis

# Base URL from where to download the oCIS binary
ocis_download_url: 'https://download.owncloud.com/ocis/ocis'

# Whether oCIS will generate self-signed certificates or not
ocis_env_insecure: false

# Log level such as 'warn' or 'debug'
ocis_env_log_level: warn

# Interface and port to which oCIS binds to
ocis_env_proxy_http_address: '0.0.0.0:9200'

# Whether the proxy takes care of TLS termination or not
ocis_env_proxy_tls: false

# URL where oCIS will be available from
ocis_env_url: 'https://ocis.example.com'

# System group used for the oCIS processes
ocis_group: ocis

# System user used for the oCIS processes
ocis_user: ocis

# Release such as 'stable' or 'testing' to install
# See also https://download.owncloud.com/ocis/ocis/
ocis_release: stable

# Systemd service 'Requires=' unit dependency to depend on a separate mount
# point (e.g. var-lib-ocis.mount)
ocis_systemd_requires:

# Exact version to install
# See also https://download.owncloud.com/ocis/ocis/
ocis_version: 4.0.2
```

Another option is to use `ansible-doc` to read the argument specification:

```sh
ansible-doc --type role -r roles -e main ocis
```

## Requirements

This roles has no additional requirements.

## License

See [LICENSE](./LICENSE)

## Author Information

[Karras](https://github.com/karras)
