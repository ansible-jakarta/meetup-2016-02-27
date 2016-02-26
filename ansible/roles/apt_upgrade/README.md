# apt_upgrade #

Equivalent of running `aptitude update` followed by `aptitude safe-upgrade`, `aptitude full-upgrade` or `apt-get dist-upgrade` on the system.

Default is concervative `safe` upgrade, but on brand new systems `full` upgrade is probably more appropriate.

## Requirements ##

In order to run safe or full upgrade, aptitude must be installed on the system.

## Role Variables ##

    - name: apt_cache_valid_time
      desc: apt cache validity in seconds
      value:
    - name: apt_upgrade_type
      desc: type of upgrade to run (safe, full, dist)
      default: safe

## Dependencies ##

None.

## Example Playbook ##

    - hosts: servers
      roles:
         - role: apt_upgrade
           apt_upgrade_type: full
