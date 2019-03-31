# Ansible Role: Docker Host

Ansible Role for setting up a Docker host, mostly for testing purposes.

The existence of this role is not an indication that an existing Ansible role
was not available, but is instead an attempt to better learn the process of
developing and using Ansible roles. There are likely better roles available
for your purposes, but please feel free to use this role and open issues with
suggestions for improvement.

## Limitations

Currently this role has only been tested on Ubuntu 16.04+ systems. Broader support is planned for future releases.

## Requirements

The target system is currently assumed to be an Ubuntu 16.04 or newer system,
likely a virtual machine. Future efforts should extend this role to also
support CentOS and/or Red Hat systems.

## Role Variables

All variables are set within `default/main.yml`.

|             Variable              |                                          Purpose                                          |
| --------------------------------- | :---------------------------------------------------------------------------------------- |
| `base_packages`                   | List of base or "core" packages needed by this role                                       |
| `docker_related_distro_packages`  | List of Docker packages to be installed from the official repo                            |
| `docker_related_python_modules`   | Python modules installed from PyPi to provide Docker management functionality             |
| `docker_apt_repo_key_fingerprint` | Packaging signing key fingerprint. Used to fetch GPG package signing key from key server. |
| `key_server`                      | GPG public key server which can be used to retrieve the key used to sign Docker packages  |
| `docker_apt_repo`                 | APT `sources.list.d` template used to allow package installation from upstream repo       |
| `docker_users`                    | List of users that should be added to the `docker` user group                             |

## Dependencies

None

## Example Playbook

```yaml
- name: Configure Docker host
  hosts: docker-hosts
  connection: local

  gather_facts: yes

  tasks:

      - name: Install Docker packages, perform initial setup
        import_role:
          name: atc0005.docker-host
```

## Installing the role

### Create `requirements.yml` file

Note: This role is not yet availalble via Ansible Galaxy, so for now you will
need to install it via a `requirements.yml` file.

#### Specific stable release version

```yaml
---

- name: "atc0005.docker-host"
  src: https://github.com/atc0005/ansible-role-docker-host.git"
  version: "v1.0"

...

```

#### Latest from the `master` branch

Example `requirements.yml` file that uses the latest from the `master` branch:

```yaml
---

- name: "atc0005.docker-host"
  src: https://github.com/atc0005/ansible-role-docker-host.git"
  version: "master"

...

```

### Use `requirements.yml` file to install role

#### Option 1: Within your home directory

- `ansible-galaxy install -r requirements.yml`

#### Option 2: Within a `roles` directory in the same location as your playbooks

- `ansible-galaxy install -r requirements.yml -p roles`

#### Option 3: System-wide for all users

- `sudo ansible-galaxy install -r requirements.yml`

## License

MIT

## Author Information

This role was created in 2019 by Adam Chalkley as part of building an on-demand
development environment toolkit managed by Ansible.

## References

- <https://github.com/atc0005/ansible-playbooks>
- <https://github.com/atc0005/ansible-role-lxd-host>
- <https://github.com/atc0005/ansible-role-lxd-testenv>
- <https://github.com/atc0005/ansible-role-docker-host>
