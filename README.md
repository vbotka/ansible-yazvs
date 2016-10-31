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

Fit cron command to your needs (see Note).

```
bsd_yazvs_cron_command: "/root/bin/yazvs.pl -u -a example.com.ksk -e 7 -m lax.xfr.dns.icann.org example.com"
```

TBD (Check defaults).


Dependencies.
------------

None.


Note
----

Example to extract KSK from the tested zone.

```
> dig @lax.xfr.dns.icann.org example.com axfr > example.com
> dig example.com dnskey | awk '$5 == 257' > example.com.ksk
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

