YAZVS (Yet Another Zone Validation Script)
==========================================

[![Build Status](https://travis-ci.org/vbotka/ansible-yazvs.svg?branch=master)](https://travis-ci.org/vbotka/ansible-yazvs)

[Ansible role.](https://galaxy.ansible.com/vbotka/yazvs/) Install YAZVS (Yet Another Zone Validation Script) from [yazvs.verisignlabs.com](http://yazvs.verisignlabs.com/). Optionaly configure cron to check DNSSEC.


Requirements.
------------

None.


Role Variables.
--------------

Set bsd_yazvs_cron to enable cron.

```
bsd_yazvs_cron: "yes"
```

Fit cron command to your needs. Review the template Validate-DNS.j2 and related bsd_Validate_DNS_* variables.

```
bsd_yazvs_cron_command: "Validate-DNS.sh"
```

TBD (Check defaults).


Dependencies.
------------

None.


Workflow
--------

1) Change shell to /bin/sh.

```
ansible host -e 'ansible_shell_type=csh ansible_shell_executable=/bin/csh' -a 'sudo pw usermod user -s /bin/sh'
```

2) Install role.

```
ansible-galaxy install vbotka.yazvs
```

3) Fit variables.

```
~/.ansible/roles/vbotka.yazvs/vars/main.yml
```

4) Create playbook.

```
> cat ~/.ansible/playbooks/freebsd-yazvs.yml
---
- hosts: example.com
  become: yes
  become_method: sudo
  roles:
    - role: vbotka.yazvs
```

5) Install and configure yazvs.

```
ansible-playbook ~/.ansible/playbooks/freebsd-yazvs.yml
```


Example how to run yazvs.pl
---------------------------

```
dig @lax.xfr.dns.icann.org example.com axfr > example.com
dig example.com dnskey | awk '$5 == 257' > example.com.ksk
yazvs.pl -u -a example.com.ksk -e 7 -m lax.xfr.dns.icann.org example.com
```


References
----------

- [YAZVS — Yet Another Zone Validation Script](http://yazvs.verisignlabs.com/)


License.
-------

[![license](https://img.shields.io/badge/license-BSD-red.svg)](https://www.freebsd.org/doc/en/articles/bsdl-gpl/article.html)


Author Information.
------------------

[Vladimir Botka](https://botka.link)

