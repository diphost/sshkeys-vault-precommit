sshkeys-vault-precommit - git pre-commit hook
=============================================

Git pre-commit hook for simple ssh-keys git repository (ssh-keys vault).
Script parses YAML configuration file and compiles per host YAML configurations that includes the required keys.
Allows to add, remove keys and persons, grant and revoke access to different users different hosts

Uses by https://github.com/diphost/ansible-role-sshkey-access-provisioning for example

Features
--------

* Many persons for many users for many hosts
* Multiple ssh keys for any person
* Python 2.7+ and 3.1+ compatible


Use
---

* Create required directory structure
* Put pre-commit script to _bin_ subdirectory. You can use git submodules to for script maintance
* Create _conf/config.yml_ with your inventory
* Add persons keys
* Init git repository
* Create symlink to pre-commit hook:
```shell
  cd .git/hooks
  ln -s ../../bin/pre-commit
```
* Commit changes
* Adds, removes keys, change config.yml if needed
* Commit changes

Directory structure
-------------------

```
bin/
\____ pre-commit        # source of pre-commit hook
conf/
\____ config.yml        # configuration file
host_confs/             # directory to result host configurations, one per host
keys/
\____ ashot/
      \_____ home.rsa   # public keys, one per file, openssh format
      \_____ home.ecdsa
\____ givi/
      \____ home.ecdsa
      \____ office.rsa
      \____ office.ecdsa
```

--
[![LICENSE WTFPL](wtfpl-badge-1.png)](LICENSE)

