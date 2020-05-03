# YAZVS (Yet Another Zone Validation Script)

[![Build Status](https://travis-ci.org/vbotka/ansible-yazvs.svg?branch=master)](https://travis-ci.org/vbotka/ansible-yazvs)

[Ansible role.](https://galaxy.ansible.com/vbotka/yazvs/) Install YAZVS (Yet Another Zone Validation Script) from [yazvs.verisignlabs.com](http://yazvs.verisignlabs.com/). Optionaly configure cron to check DNSSEC.

Feel free to [share your feedback and report issues](https://github.com/vbotka/ansible-yazvs/issues). Contributions are welcome.


## Requirements

None.


## Role Variables

Set *bsd_yazvs_cron* to enable cron.

```
bsd_yazvs_cron: true
```

Fit cron command to your needs:

- Review the template Validate-DNS.j2
- Review related bsd_Validate_DNS_* variables
- Review options of yazvs.pl

```
bsd_yazvs_cron_command: "Validate-DNS.sh"
```

Review defaults and examples in vars.


## Dependencies

None.


## Workflow

1) Change shell to /bin/sh

```
shell> ansible host -e 'ansible_shell_type=csh ansible_shell_executable=/bin/csh' -a 'sudo pw usermod user -s /bin/sh'
```

2) Install role

```
shell> ansible-galaxy install vbotka.yazvs
```

3) Fit variables

```
shell> editor vbotka.yazvs/vars/main.yml
```

4) Create playbook

```
shell> cat freebsd-yazvs.yml
- hosts: srv.example.com
  roles:
    - vbotka.yazv
```

5) Install and configure yazvs

```
shell> ansible-playbook freebsd-yazvs.yml
```


## Example how to run yazvs.pl

```
shell> dig @lax.xfr.dns.icann.org example.com axfr > example.com
shell> dig example.com dnskey | awk '$5 == 257' > example.com.ksk
shell> yazvs.pl -u -a example.com.ksk -e 7 -m lax.xfr.dns.icann.org example.com
```


## References

- [YAZVS — Yet Another Zone Validation Script](http://yazvs.verisignlabs.com/)


## License

[![license](https://img.shields.io/badge/license-BSD-red.svg)](https://www.freebsd.org/doc/en/articles/bsdl-gpl/article.html)


## Author Information

[Vladimir Botka](https://botka.link)
