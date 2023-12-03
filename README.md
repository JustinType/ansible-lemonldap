Ansible LemonLDAP::NG role
=========

This is the ansible LemonLDAP::NG role. It can be used to install LemonLDAP::NG on a server.

Requirements
------------

Pulling packages from the LLNG repository, which is to be installed by this role.

Role Variables
--------------

 * `lemonldap_do_soap`, toggles SOAP-related webserver configuration, defaults to `False`.
 * `lemonldap_domain`, the root domain of your LLNG setup, defaults to `changeme.com`.
 * `lemonldap_webserver`, the webserver running LLNG, defaults to `nginx`, could be changed to `apache`.

LDAP Variables
--------------

 * `ldap_server_ip`, Ip of your ldap server (i.e: `"ldap://192.168.1.5"`)
 * `ldap_port`, 389 = ldap / 636 = ldaps
 * `ldap_verification`, can be require, optional, none (for ldaps you need require)
 * `ldap_timeout`, timeout before ldap deconnexion (recommended: 60 or 120)
 * `ldap_base`, base for ldap search queries (i.e: `"dc=domain,dc=local"`)
 * `ldap_account`, account used for ldap authentication (i.e: `"cn=websso,cn=users,dc=domain,dc=local"`)
 * `ldap_password`, 389 = password of this account


Dependencies
------------

None

Example Playbook
----------------

```
  - name: Install LemonLDAP
    hosts: localhost
    become: yes
    roles:
      - role: ansible-lemonldap
        lemonldap_domain: localhost
        lemonldap_webserver: "apache"
    vars:
      - ldap_server_ip: "ldap://192.168.1.2"
      - ldap_port: 389 
      - ldap_verification: "none"
      - ldap_timeout: 120
      - ldap_base: "dc=mysuper,dc=domain"
      - ldap_account: "cn=websso,cn=users,dc=mysuper,dc=domain"
      - ldap_password: "SuperP@ssw0rd!"
```

License
-------

MIT

Author Information
------------------

See [AUTHORS](AUTHORS)
