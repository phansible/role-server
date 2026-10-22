# Phansible Role: Server

[![CI](https://github.com/phansible/role-server/actions/workflows/ci.yml/badge.svg)](https://github.com/phansible/role-server/actions/workflows/ci.yml)

An Ansible Role that installs base packages and sets the timezone and locale on Ubuntu and Debian, created with [Phansible](http://phansible.com/) in mind.

## Requirements

- Ubuntu 22.04, 24.04, 26.04 or Debian 12, 13 (x86_64)
- Ansible >= 2.15 with the `community.general` collection (bundled with the `ansible` package, install it separately if you only have `ansible-core`)
- Root access or `become` on the target

## Role Variables

All settings live in a single `server` dictionary, defined in `defaults/main.yml`:

```yaml
server:
  timezone: UTC
  locale: en_GB.UTF-8
  packages: []
```

| Key | Default | Description |
| --- | --- | --- |
| `server.timezone` | `UTC` | Name under `/usr/share/zoneinfo`, written to `/etc/timezone` and linked to `/etc/localtime` |
| `server.locale` | `en_GB.UTF-8` | Locale generated with `locale-gen` (it is not set as the system default) |
| `server.packages` | `[]` | Extra apt packages to install at their latest version |

`curl`, `wget`, `ca-certificates`, `tzdata` and `locales` are always installed. Ansible replaces dictionaries rather than merging them, so when you override `server` set all three keys.

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  become: yes
  vars:
    server:
      timezone: Europe/London
      locale: en_GB.UTF-8
      packages: [git, vim]
  roles:
    - role-server
```

## License

This role is released under the terms of the license specified in the repository or if not specified, under the [MIT license](https://raw.githubusercontent.com/phansible/role-server/master/LICENSE).

## Author Information

This role was created in 2015 by [The Phansible Team & Contributors](https://github.com/phansible/role-server/graphs/contributors), credits go also to [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/) and source of inspiration.
