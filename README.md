Unix Users Setup
=========

This role can be used to create Unix users and assign them to groups.

[![Build Status](https://travis-ci.org/Rheinwerk/ansible-role-unix_users.svg?branch=master)](https://travis-ci.org/Rheinwerk/ansible-role-unix_users)

Requirements
------------

None.

Role Variables
--------------

There is one main variable that drives this role: `_unix_users`. It is a map that contains all configuration and settings for this role.
Please see `defaults/main.yml` for details.

Dependencies
------------

None.


Example Playbook
----------------

The general contract of this role is to take the variables map `_unix_users` from `defaults/main.yml` as a template for your configuration and pass that configuration as a parameter to this role.

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      var:
        UNIX_USERS:
          ...
      roles:
         - { role: unix_users, tags: [ 'unix_users' ], _unix_users: "{{ UNIX_USERS }}" }

License
-------

Please see LICENSE.

Author Information
------------------

Original author is [Daniel Schneller](https://github.com/dschneller) as member of the [Rheinwerk](https://github.com/Rheinwerk) project.

