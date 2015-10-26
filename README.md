ssh-keys-vault - scheme for ssh-keys repository on git
======================================================

Simple scheme for ssh-keys repository on git. Include pre-commit hook to compile YAML host configusration file for https://github.com/diphost/ansible-role-sshkey-access-provisioning

WARNING
-------

This is a scheme for store and manage really public ssh keys and hosts inventory. Consider this.

Features
--------

* Many persons for many users for many hosts
* Multiple ssh keys for any person
* Python 2.7+ and 3.1+ compatible

Directory structure
-------------------

bin/
\____ pre-commit        # source of pre-commit hook
conf/
\____ config.yml        # configuration file
\____ config.yml.sample # configuration example
host_confs/             # directory to result host configurations, one per host
keys/
\____ alice/
      \_____ home.rsa   # public keys, one per file, openssh format
      \_____ home.ecdsa
\____ givi/
      \____ home.ecdsa
      \____ office.rsa
      \____ office.ecdsa

Host configuration sample
-------------------------

```yml
---
hosts:
        - host: host.example.com
          users:
                - user: admin
                  authorized:
                        - person: alice
                        - person: givi
```

Result host configuration sample
--------------------------------

```yml
---
users:
- algs:
  - authorized:
    - ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAuCZ1ovq6lUwc9me1ENX/Jw7VrDbpIJt8h0c7K25puFLPI9d45HyQNbHYaxy4Arl3yft5JjnOqm8ERDs9Gy0H8RGBBX1/+EhnM/SFyJ7J9+qF0EAgGGF7ID6XDXyXQxilYn6R7mDz02ZCuQtLFY9VGF5lfWKWR10soId+FdIW9prEVHHWSHZnXuc90z0PFarFD4m9vbgK534X/oEDuc2tIkUvOeZomcJaJ/3oVMP4IFpqbTBnf1BuCc1QvywPcjzOCxqkon05Vf5Xi5gfPFJRTkO+CyfqkcACevTuqNWix6623Nte605pNMXmeEoiUcBbI4n5HjUz2x11yGZq2hy6zp==
      alice@home
    - ssh-rsa AAAAB3NzaC1yc2EAATTBIwAAAQEAuCZ1ovq6lUwc9me1ENX/JrWVrDbpIJX8h0c7K25puFLPI9d45HyQNbHYaxy4Arl3yft5JjnOqm8ERDs9Gy0H8RGBBX1/+EhnM/SFyJ7J9+qF0EAgGGF7ID6XDXyXQxilYn6R7mDz02ZCuQtLFY9VGF5lfWKWR10soId+FdIW9prEVHHWSHZnXuc90z0PFarFD4m9vbgK534X/oEDuc2tIkUvOeZomcJaJ/3oVMP4IFpqbTBnf1BuCc1QvywPcjzOCxqkon05Vf5Xi5gfPFJRTkO+CyfqkcACevTuqNWix6623Nte605pNMXmeEoiUcBbI4n5HjUz2x11yGZq2hytEQ==
      givi@office
    name: rsa
  - authorized:
    - ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNWYAAAAIbmlzdHAyNTYAAABBBGbzAPb3aMuBLxMFjEacJeMGan+b4zA3cv4JHyUCyM3nsRmWIcK7zMeN1nbtIk4ywkzs/6/Ya1aqjB47SUwItPY=
      givi@home
    - ecdsa-sha2-nistp256 AAAAE2VeZHNhLXToYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBImELZAlFb5wrVFFFWPs/3Yz4kNT1Gs2Y5JW6gVTmC4fGX2WCYEYWcKL4mBNfzWkgfADsYaWTQieYhqOmu675EW=
      givi@office
    name: ecdsa
  user: admin
```


--
[![LICENSE WTFPL](wtfpl-badge-1.png)](LICENSE)

