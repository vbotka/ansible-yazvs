# yazvs

[![quality](https://img.shields.io/ansible/quality/27910)](https://galaxy.ansible.com/vbotka/yazvs)[![Build Status](https://app.travis-ci.com/vbotka/ansible-yazvs.svg?branch=master)](https://app.travis-ci.com/vbotka/ansible-yazvs)[![GitHub tag](https://img.shields.io/github/v/tag/vbotka/ansible-yazvs)](https://github.com/vbotka/ansible-yazvs/tags)

[Ansible role.](https://galaxy.ansible.com/vbotka/yazvs/) Install YAZVS (Yet Another Zone Validation Script) from [github.com/verisign/yazvs](https://github.com/verisign/yazvs/). Optionally, configure cron to check DNSSEC.

Feel free to [share your feedback and report issues](https://github.com/vbotka/ansible-yazvs/issues).

[Contributions are welcome](https://github.com/firstcontributions/first-contributions).


## Requirements

### Collections

- community.general


## Role variables

See the variables in defaults/main.yml. Set *bsd_yazvs_cron* to enable cron

```bash
bsd_yazvs_cron: true
```

Fit cron command to your needs:

* Review the template Validate-DNS.j2
* Review related variables bsd_validate_dns_*
* Review options of yazvs.pl

```bash
bsd_yazvs_cron_command: "Validate-DNS.sh"
```


## Workflow

1) Change shell on the remote host to /bin/sh if necessary

```bash
shell> ansible host -e 'ansible_shell_type=csh ansible_shell_executable=/bin/csh' -a 'sudo pw usermod user -s /bin/sh'
```

2) Install the role and collection

```bash
shell> ansible-galaxy role install vbotka.yazvs
```

Install the collection if necessary

```bash
shell> ansible-galaxy collection install community.general
```

3) Fit variables


4) Create playbook

```bash
shell> cat freebsd-yazvs.yml
- hosts: srv.example.com
  roles:
    - vbotka.yazv
```

5) Install and configure yazvs

```bash
shell> ansible-playbook freebsd-yazvs.yml
```


## Example on how to run yazvs.pl


```bash
shell> dig @lax.xfr.dns.icann.org example.com axfr > example.com
shell> dig example.com dnskey | awk '$5 == 257' > example.com.ksk
shell> yazvs.pl -u -a example.com.ksk -e 7 -m lax.xfr.dns.icann.org example.com
```


## Ansible lint

Use the configuration file *.ansible-lint.local* when running *ansible-lint*. Some rules might be disabled and some warnings might be ignored. See the notes in the configuration file.

```bash
shell> ansible-lint -c .ansible-lint.local
```

## References

* [YAZVS — Yet Another Zone Validation Script](http://yazvs.verisignlabs.com/)


## License

[![license](https://img.shields.io/badge/license-BSD-red.svg)](https://www.freebsd.org/doc/en/articles/bsdl-gpl/article.html)


## Author Information

[Vladimir Botka](https://botka.info)
