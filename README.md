ansible-sudo-ldap
===================

A playbook for sudo administration with ldap server.

## Overview

It will install OpenLDAP and sudo management settings. You can customize it by edit vars file.

## Usage

- Edit vars/main.yml

- Test on Vagrant virtual machine(Requires Ansible).

```bash
$ vagrant up
$ vagrant ssh
[vagrant@vagrant ~]$ sudo su
[root@vagrant ~]$ su - test
[test@vagrant ~]$ sudo cat /var/log/secure 
"Enter [test]'s Password:" [Enter ldap_password defined in above]
```

- Install to remote server.

Edit `ansible_hosts`.

```
default ansible_ssh_host=127.0.0.1 ansible_ssh_port=22
```

Run playbook.

```bash
ansible-playbook site.yml -i ansible_hosts
```

## vars

```vars/main.yml
# ldap server settings
ldap_tld: com
ldap_dc: example
ldap_suffix: "dc={{ ldap_dc }},dc={{ ldap_tld }}"
ldap_root_dn: "cn=Directory Manager,{{ ldap_suffix }}"
ldap_root_password: password
ldap_dir: /var/lib/ldap

ldap_sampleuser_name: test
ldap_sampleuser_password: password

ldap_samplegroup_name: members

ldap_users_ou: people
ldap_group_ou: groups

ldap_sudoers_ou: SUDOers
ldap_sudoers_base: "ou={{ ldap_sudoers_ou }},{{ ldap_suffix }}"

# client side settings
ldap_server_uri: ldap://127.0.0.1:389
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
