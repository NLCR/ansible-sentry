Sentry
=========

Role installs sentry to localhost:9000 and supervisor to localhost:9001

Requirements
------------

PostgreSQL and Redis

```
ansible-galaxy install NLCR.sentry NLCR.postgresql NLCR.redis
```

Role Variables
--------------

defaults/main.yml
```
sentry:
  # supervisor will run sentry with this user
  user: vagrant
  group: vagrant

  # hostname
  hostname: '{{ ansible_nodename }}'
  port: 9000

  # sentry secret for connection with app, A new key can be generated with `$ sentry config generate-secret-key`
  secret: "*nk=yh)t#^=%-rkeopyr@4u@2(fy6o-!upuv2%dncez12j$yj="

  # mail server
  smtp: '{{ ansible_nodename }}'
  mail: 'sentry@{{ ansible_nodename }}'

  # PostgreSQL
  db_user: vagrant
  db_pass: vagrant
  db_name: sentry
  db_host: '{{ ansible_nodename }}'
  db_port: 5432

  # Redis
  redis_host: '{{ ansible_nodename }}'
  redis_port: 6379
```

Dependencies
------------

NLCR.supervisor

Example Playbook
----------------

Simples example
```
- name: Database playbook
  hosts: database
  roles:
  - { role: NLCR.postgresql, postgresql: [{ user: vagrant, pass: vagrant, db: sentry }] }
  - { role: NLCR.redis }
  - { role: NLCR.sentry, sentry: { user: vagrant, db_user: vagrant, db_pass: vagrant, db_name: sentry } }
```

Sentry and databases separated
```
- name: Database playbook
  hosts: database
  roles:
  - { role: NLCR.postgresql, postgresql: [{ user: vagrant, pass: vagrant, db: sentry }] }
  - { role: NLCR.redis }

- name: Application playbook
  hosts: app
  roles:
  - { role: NLCR.sentry, sentry: { user: vagrant, port: 9000, db_user: vagrant, db_pass: vagrant, db_name: sentry, redis_host: 127.0.0.1, redist_port: 6379 } }
```
License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
