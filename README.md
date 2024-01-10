Ansible LemonLDAP::NG role
=========

This is the ansible LemonLDAP::NG role. It can be used to install LemonLDAP::NG on a server.

Installation
------------

Installation of ansible
```
sudo apt install ansible
```

Creation of ansible role repository
```
cd /home/[user]
mkdir .ansible
mkdir .ansible/roles
```

Get ansible profile
```
cd .ansible/roles
git clone https://github.com/JustinType/ansible-lemonldap
```

Move and edit playbook
```
cd ..
mv roles/ansible-lemonldap/playbook.yaml .
nano playbook.yaml
```

[Optional] Create skin customization folder and put your files here
```
cd roles/ansible-lemonldap
mkdir skin_customization
```

Run playbook
```
ansible-playbook playbook.yaml
```

Configuration: Role Variables
--------------

 * `lemonldap_do_soap`, toggles SOAP-related webserver configuration, defaults to `False`.
 * `lemonldap_domain`, the root domain of your LLNG setup, defaults to `changeme.com`.
 * `lemonldap_webserver`, the webserver running LLNG, defaults to `nginx`, could be changed to `apache`.

Configuration: LDAP Variables
--------------

 * `ldap_server_ip`, Ip of your ldap server (i.e: `"ldap://192.168.1.5"`)
 * `ldap_port`, 389 = ldap / 636 = ldaps
 * `ldap_verification`, can be "require", "optional", "none" (if you use a auto-signed certificate for ldaps put "none" or "optional" because lemonladp will not be able to verify your certificate, else it is recommended to put "require")
 * `ldap_timeout`, timeout before ldap deconnexion (recommended: 60 or 120)
 * `ldap_base`, base for ldap search queries (i.e: `"dc=domain,dc=local"`)
 * `ldap_account`, account used for ldap authentication (i.e: `"cn=websso,cn=users,dc=domain,dc=local"`)
 * `ldap_password`, password of this account

Configuration: Skin Customization [Optional]
--------------

If you don't want to customize these options, let the value "default"
Else, all these files must be located in /home/[user]/.ansible/roles/ansible-lemonldap/skin_customization (you have to create this folder)

 * `custom_main_logo`, filename of your custom logo (will be included in portal template and mail body)
 * `custom_favicon`, filename of your custom favicon
 * `custom_background`, filename of your custom background


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
      - main_logo: "logo.png"
      - favicon: "favicon.ico"
      - background: "background.png"
```

License
-------

MIT

Author Information
------------------

See [AUTHORS](AUTHORS)
