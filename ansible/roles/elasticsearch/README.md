# shared/elasticsearch #

Installs elasticsearch 2.x

## Requirements ##

Ansible 2.0

## Role Variables ##

See : `defaults/main.yml`

## Dependencies ##

    - role: java_openjdk

## Example Playbook ##

    - hosts: servers
      roles:
         - role: elasticsearch
