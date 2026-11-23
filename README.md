Unix Users Setup
=========

This role can be used to create Unix users and assign them to groups.

[![Build Status](https://github.com/Rheinwerk/ansible-role-unix_users/actions/workflows/ci.yml/badge.svg)](https://github.com/Rheinwerk/ansible-role-unix_users/actions/workflows/ci.yml)

It also adds `%admin ALL = NOPASSWD: ALL` to `/etc/sudoers` (checked with `visudo`).

Requirements
------------

`sudo` (`visudo`) on the target.

Role Variables
--------------

Every variable has a default (`defaults/main.yml`); set only the ones that differ.
`meta/argument_specs.yml` and `tasks/assert.yml` check the values before anything
is changed.

| Variable | Default | Description |
| --- | --- | --- |
| `_unix_users_groups` | one system group `"{{ CENTERDEVICE.group }}"` | Groups to create, see below. |
| `_unix_users_users` | one user `"{{ CENTERDEVICE.user }}"`, comment `CenterDevice User`, groups `["{{ CENTERDEVICE.group }}"]`, shell `/usr/sbin/nologin` | Users to create or remove, see below. |

The defaults read the CenterDevice consumer contract (`CENTERDEVICE.user`,
`CENTERDEVICE.group`); a play without it sets both variables itself.

Group keys:

| Key | Required | Description |
| --- | --- | --- |
| `name` | yes | Group name, unique. |
| `system` | no | System group, default `false`. |
| `gid` | no | Group ID. |

User keys:

| Key | Required | Description |
| --- | --- | --- |
| `name` | yes | User name, unique. |
| `comment` | for present users | GECOS field, one line. |
| `groups` | for present users | Supplementary groups, they must exist. |
| `uid` | no | User ID. |
| `password` | no | Password hash, default `!` (locked). |
| `shell` | no | Absolute path, default `/bin/bash`. |
| `ssh.public_key` | no | Written to `~/.ssh/authorized_keys`. |
| `state` | no | `present` (default) or `absent`; absent removes the user and its home directory. |

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: servers
      vars:
        _unix_users_groups:
          - { name: app, system: true, gid: 50000 }
        _unix_users_users:
          - name: app
            comment: App user
            uid: 50000
            groups: [app]
            shell: /usr/sbin/nologin
      roles:
        - { role: unix_users, tags: ['unix_users'] }

License
-------

Please see LICENSE.

Author Information
------------------

Original author is [Daniel Schneller](https://github.com/dschneller) as member of the [Rheinwerk](https://github.com/Rheinwerk) project.
