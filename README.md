marcusianlevine.rename-database
=========

[![Build Status](https://travis-ci.org/marcusianlevine/ansible-role-rename-database.svg?branch=perms)](https://travis-ci.org/marcusianlevine/ansible-role-rename-database)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-marcusianlevine.rename--database-660198.svg?style=flat)](https://galaxy.ansible.com/marcusianlevine/rename-database)

Small utility role to create, rename, and swap databases on a remote database server (currently only targets PostgreSQL)

Requirements
------------

Utilizes the `postgresql_` Ansible modules, which require psycopg2 to be installed on the host running this role.

Role Variables
--------------

### Required
- `db_host`: hostname of the remote database server to operate on
- `db_port`: port that the database server accepts connections on
- `login_user`: connect to the remote database with this username
- `login_password`: connect to the remote database with this password _(NOTE: Use ansible-vault to provide this value from an encrypted file! Don't store your database password unencrypted in your repo!)_
- `databases`: list of dictionaries describing the databases which will be created/renamed/swapped. Should have the following items:
  - `target`: name of the database .
  - `replacement`: current name of the database which will replace `target`.
  - `new_target_name`: Optionally specify the new name which `target` should be given after being replaced by `replacement`. (see `defaults/main.yml` for default prefix and suffix used if not specified)
- `db_owner`: name of role/user on remote database server that should own the databases created by this role. Defaults to `login_user`
- `swap_db`: failsafe control variable to prevent accidental swaps. In order to swap/replace the targets with their replacements, you must set this variable to be truthy.
- `keep_replacement`: by default, this role recreates the original databases after they are renamed. Set this to false to disable.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: localhost 
      roles:
         - role: marcusianlevine.rename-database
           db_host: db.example.co
           login_user: myuser
           login_password: secret
           target_db: my_target
           replacement_db: my_staging_db
           swap_db: yes

License
-------

BSD

Author Information
------------------

Written by Marcus Levine for CKM Advisors