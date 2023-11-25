# Ansible Role - traefik

Manages and deploys Traefik.

**Note:** When configuring Let's Encrypt based on the DNS challenge, it's
recommended to store the appropriate access token for the DNS provider in a
separate file. The file path (e.g. `/etc/traefik/token`) can then be injected
via the systemd service file for Traefik (see the role variables). This way the
token is not exposed directly in any environment variables. See also [Traefik -
DNS Challenge Providers](https://doc.traefik.io/traefik/https/acme/#providers).

# Example: 

## Example Playbook

As this role is tested via Molecule one can use [that
playbook](./molecule/default/converge.yml) as a starting point:

```yaml
---

- name: Converge
  hosts: all
  gather_facts: true

  roles:
    - role: traefik
```

## Role Variables

The default variables are defined in [defaults/main.yml](./defaults/main.yml):

```yaml
# File where ACME data is stored
traefik_acme_file: '{{ traefik_config_path }}/acme.json'

# Main configuration based on 1:1 dict copy of the intended Traefik config
# Full blown example:
# traefik_config:
#   global:
#     checkNewVersion: false
#     sendAnonymousUsage: false
#   entryPoints:
#     web:
#       address: ':80'
#       http:
#         redirections:
#           entryPoint:
#             to: websecure
#             scheme: https
#     websecure:
#       address: ':443'
#   certificatesResolvers:
#     myresolver:
#       acme:
#         email: ''
#         storage: '{{ traefik_acme_file }}'
#         dnsChallenge:
#           provider: cloudflare
traefik_config: {}

# Directory where to place the Traefik configs
traefik_config_path: /etc/traefik

# Systemd service environment configuration
# Used for setting lego environment variables to point to the appropriate
# secrets file with the goal to automate the Let's Encrypt DNS verification
# Example: CF_API_EMAIL_FILE=/etc/traefik/acme_token
traefik_environment: []

# System group used for the Traefik processes
traefik_group: traefik

# Directory where to place the Traefik logs
traefik_log_path: /var/log/traefik

# Provider configuration based on 1:1 dict copy of the intended Traefik config
# Full blown example:
# traefik_provider:
#   http:
#     routers:
#       ocis:
#         rule: Host(`example.com`)
#         service: backend
#         tls:
#           certResolver: myresolver
#     services:
#       backend:
#         loadBalancer:
#           servers:
#             - url: 'http://127.0.0.1:8080/'
traefik_provider: {}

# System user used for the Traefik processes
traefik_user: traefik
```

Another option is to use `ansible-doc` to read the argument specification:

```sh
ansible-doc --type role -r roles -e main traefik
```

## Requirements

This roles has no additional requirements.

## License

See [LICENSE](./LICENSE)

## Author Information

[Karras](https://github.com/karras)
