[ ![Image](https://cloud.githubusercontent.com/assets/5514990/24834935/e0d1db04-1d1c-11e7-8ad0-53fd45ff13c3.png "Ansible") ](https://www.ansible.com/ "Ansible")

[![Build Status](https://travis-ci.org/ansyble/role-postgres.svg?branch=master)](https://travis-ci.org/ansyble/role-postgres)
[![Ansible Role](https://img.shields.io/ansible/role/17044.svg)](https://galaxy.ansible.com/ansyble/postgres/)

[Ansible](http://www.ansible.com) role to deploy Postgres cluster.

### Install

```sh
ansible-galaxy install ansyble.postgres
```

### Usage

```yml
postgres_databases:
  - name: pg.master
    volumes:
      - pg.master:/var/lib/postgresql/data
    ports:
      - 5442:5432
    networks:
      - postgres
    env:
      POSTGRES_PASSWORD: pgpass
      DB_NAME: mydb
      DB_USER: me
      DB_PASSWORD: "{{ postgres_mydb_pass }}"
      REPLICATION_USER: replica
      REPLICATION_PASS: "{{ postgres_replica_pass }}"

  - name: pg.slave
    volumes:
      - pg.slave:/var/lib/postgresql/replica
    env:
      POSTGRES_PASSWORD: "{{ postgres_slave_pass }}"
      REPLICATION_MODE: slave
      REPLICATION_USER: replica
      REPLICATION_PASS: "{{ postgres_replica_pass }}"
      REPLICATION_HOST: pg.master
```

### Defaults

```yml
postgres_image_name: mongkok/postgres:9.6
postgres_network_name: postgres
```
