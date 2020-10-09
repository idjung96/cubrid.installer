CUBRID.Installer
=========

This role is for building a CUBRID High Availability (HA) cluster.
This role supports the follows.
 - Build environments on the servers belong to CUBRID HA cluster
 - Copy the configuration file created by CUBRID conf generator to all servers
 - start CUBRID HA Cluster
 - check if the cluster works

It is recommended to use this playbook with the [CUBRID Conf generator](https://github.com/idjung96/CUBRID_conf_generator). 
Demonstration: ([Youtube link](https://youtu.be/NWvkxOe3CLk), Korean subtitles)

Please read how to use CUBRID conf generator & this playbook.

Requirements
------------
- CENTOS 7 or higher
- CUBRID conf generator

Role Variables
--------------
Group vars
  - cubrid_account: CUBRID operator account
  - config_dir: directories of CUBRID conf files
  - cubrid_ver: CUBRID version to install
  - db_name: database name
  - create_db: whether to create databases

Dependencies
------------
Role
- singleplatform-eng.users

Project
- [CUBRID Conf generator](https://github.com/idjung96/CUBRID_conf_generator)

Example Playbook
----------------
```
$ vi play.yml
- hosts: all
  name: cubrid installer
  vars:
# modifiable start --------------------------
    cubrid_account: "cubrid1"
    config_dir: "/root/.ansible"
    cubrid_ver: "10.2"
    db_name: basic
    create_db: true
# modifiable end ---------------------------
    cubrid_platform: "x86_64"
    groups_to_create:
      - name: "cubrid"
        gid: "10000"
    users:
      - username: "{{ cubrid_account }}"
        name: "{{ cubrid_account }}"
        group: 'cubrid'
  roles:
    - singleplatform-eng.users
    - idjung96.cubrid_installer
```

License
-------
BSD

Author Information
------------------
idjung@naver.com
