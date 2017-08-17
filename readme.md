Credentials
===================

For ansible to log in, it must have a username or use the default ssh, for privilege escalation ("become") a password is needed.

Global config
----------------

Content of all.yml:

  user_name: <default username>
  root_user: <default privileged user, normally "root">

  ansible_user: "{{user_name}}"
  ansible_become_pass: "{{root_pass}}"
  ansible_become_user: "{{root_user}}"
  ansible_become_method: "su"

For each device a password.yml file contains the machine specifics

Per device config
---------------------

Content of password.yml:

  root_pass: <password>
  user_pass: <password>
  user_name: <if not default>

Note that this file should be vaulted.

Content of pub_keys subdir is the public keys associated with a given username. The file must be called "<username>_key.pub".


Directory layout
-------------------

Directory structure is expected to be
.
├── group_vars
│   ├── all.yml
│   └── ...
├── host_vars
│   ├── server01
│   │   ├── password.yml
│   │   └── ...
│   ├── server02
│   │   ├── password.yml
│   │   └── ...
│   ├── server03
│   │   ├── password.yml
│   │   └── ...
│   ├── ...
├── inventory
└── pub_keys
    ├── root_key.pub
    ├── user01_key.pub
    ├── user02_key.pub
    ├── user03_key.pub
    └── ...
