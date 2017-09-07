marcusianlevine.rename-database
=========

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
- `target_db`: name of the database which will be created/renamed/swapped.
- `replacement_db`: current name of the database which will replace `target_db`.
- `new_target_name`: specify the new name which `target_db` should be given after being replaced by `replacement_db`. (see `defaults/main.yml` for default value)
- `db_owner`: name of role/user on remote database server that should own the databases created by this role. Defaults to `login_user`
- `swap_db`: failsafe control variable to prevent accidental swaps. In order to swap/replace `target_db` with `replacement_db`, you must set this variable to be truthy.

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