YAZVS (Yet Another Zone Validation Script)
==========================================

[![Build Status](https://travis-ci.org/vbotka/ansible-yazvs.svg?branch=master)](https://travis-ci.org/vbotka/ansible-yazvs)

[Ansible role.](https://galaxy.ansible.com/vbotka/ansible-yazvs/) Install YAZVS (Yet Another Zone Validation Script) from [yazvs.verisignlabs.com](http://yazvs.verisignlabs.com/). Optionaly configure cron to check DNSSEC.

WIP. See TODO section.


Requirements.
------------

None.


Role Variables.
--------------

Set bsd_yazvs_cron to enable cron.

```
bsd_yazvs_cron: "yes"
```

Fit default command to your needs.

```
bsd_yazvs_cron_command: "/root/bin/yazvs.pl"
```

TBD (Check defaults).


Dependencies.
------------

None.


TODO
----

Find valid command to validate DNSSEC

```
# yazvs.pl  -u -x -a /usr/local/etc/namedb/keys/dsset-example.com. -e 30 -t /usr/local/etc/namedb/keys/Kexample.com.KSK.key -n Kexamlle.com.KSK -m master /usr/local/etc/namedb/master/example.com.signed
Crypto Validation of example.com 2016102502
----------------------------------------------------------------------
OK: Parsed 34 RRs from /usr/local/etc/namedb/master/example.com.signed
OK: 1 trusted KSKs found
PROBLEM: Cannot validate DNSKEY RRset with KSKs
PROBLEM: 16 expiring RRSIGs found
OK: 0 bad RRSIGs found
PROBLEM: 0 good RRSIGs found
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
