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
The playbooks are meant to be executed from the `ansible` box.

Simple vagrant shell provisioner `install-ansible.sh` is used to automatically install latest ansible (v2.0.1) on the `ansible` box during initial bootstrap.

The `ansible` directory inside this repo is mounted as `/etc/ansible` inside the `ansible` box. Any changes you make to the files in this directory will by synced to the `ansible` box.

Port `25061` of the host machine is forwarded to the port `5601` of the `es` box.

Port `35601` of the host machine is forwarded to the port `5601` of the `kibana` box.

## Create ansible user

First we create special user named `ansible` on each box, which will be used for all future password-less provisioning.

- ssh into `ansible` box:
```
vagrant ssh ansible
```
- change permissions of the private key file, so SSH doesn't complain about it:
```
chmod 600  /etc/ansible/.ssh/id_rsa_ansible
```
- go into playbooks directory:
```
cd /etc/ansible/playbooks
```
- execute setup playbook to create ansible users, authorize our ssh key and run full system upgrade. At this point we're still using default password `vagrant` to connect to each machine:
```
ansible-playbook setup-01.yml --user vagrant --ask-pass
```

The `setup-01.yml` playbok is written without using roles. Playbook `setup-02.yml` achieves the same result, but is refactored into re-usable `ansible-users` and `apt_upgrade` roles, which you can find in `/etc/ansible/roles` directory.

## Install Java, ElasticSearch & Kibana

- view playbook-01.yml
- ansible-playbook playbook-01.yml
- compare to playbook-02.yml
