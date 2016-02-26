# shared/kibana-4.4 #

Installs latest version of Kibana from the 4.4 branch.

## Requirements ##

Ansible 2.0

## Role Variables ##

See: `defaults/main.yml`

## Dependencies ##

None.

## Example Playbook ##

    - hosts: servers
      roles:
         - role: kibana-4.4
