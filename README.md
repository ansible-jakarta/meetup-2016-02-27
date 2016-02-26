# Ansible Jakarta Meetup 2016-02-27

## Sample Playbook

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
