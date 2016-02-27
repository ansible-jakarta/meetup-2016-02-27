# Ansible Jakarta Meetup 2016-02-27

To get started run `vagrant up` to bring up three machines:

- ansible (192.168.20.10)
- es (192.168.20.20)
- kibana (192.168.20.30)

Default user:password on each box is: vagrant:vagrant

To SSH into any of the machines use:
```
vagrant ssh <box-name>
```
The playbooks are execute from the ansible box.

Simple vagrant shell provisioner `install-ansible.sh` is used to install latest ansible (v2.0.1) on the `ansible` box.

The `ansible` directory inside this repo is mounted as `/etc/ansible` inside the `ansible` box.

Port `25061` of the host machine is forwarded to the port `5601` of the `es` box.

Port `35601` of the host machine is forwarded to the port `5601` of the `kibana` box.

## Steps

- vagrant up
- vagrant ssh ansible
- cd /etc/ansible
- chmod 600 .ssh/id_rsa_ansible
- cd playbooks
- view setup-01.yml
- ansible-playbook setup-01.yml --user vagrant --ask-pass
  - password: vagrant
- compare to setup-02.yml
- view playbook-01.yml
- ansible-playbook playbook-01.yml
- compare to playbook-02.yml
