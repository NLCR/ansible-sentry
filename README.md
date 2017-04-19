Sentry
=========

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

defaults/main.yml
```
sentry_user: vagrant
sentry_port: 9000

sentry_db_user: vagrant
sentry_db_pass: sentry
sentry_db_name: sentry

sentry_secret: '*nk=yh)t#^=%-rkeopyr@4u@2(fy6o-!upuv2%dncez12j$yj=' # A new key can be generated with `$ sentry config generate-secret-key`

sentry_smtp_host: '{{ ansible_nodename }}'
sentry_mail: 'sentry@{{ ansible_nodename }}'
sentry_hostname: '{{ ansible_nodename }}'
```

Dependencies
------------

NLCR.postgresql
NLCR.supervisor

Example Playbook
----------------

- name: Sentry database
  hosts: database
  roles:
  - { role: NLCR.postgresql, postgresql: [{ user: vagrant, pass: sentry, db: sentry }] }

- name: Sentry app
  hosts: app
  roles:
  - NLCR.sentry
  - NLCR.supervisor

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
