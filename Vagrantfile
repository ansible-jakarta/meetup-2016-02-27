# -*- mode: ruby -*-
# vi: set ft=ruby :

# Override host locale in SSH session
ENV["LC_ALL"] = "en_US.UTF-8"

Vagrant.configure(2) do |config|

  # vagrant-cachier configuration
  # to install run: 'vagrant plugin install vagrant-cachier'
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :machine
    config.cache.auto_detect = true
    # optionally enable NFS to speedup virtualbox shares
    #
    # config.cache.synced_folder_opts = {
    #   type: :nfs,
    #   mount_options: ['rw', 'vers=3', 'tcp', 'nolock']
    # }
  end

  # enable host only network (needed for NFS shares)
  # config.vm.network "private_network", type: "dhcp"

  config.vm.define 'ansible' do |ansible|
    # don't check for box updates (slow)
    ansible.vm.box_check_update = false
    # specify base box
    ansible.vm.box = "ubuntu/trusty64"
    # set box hostname
    ansible.vm.hostname = "ansible"
    # create private network
    ansible.vm.network "private_network", ip: "192.168.20.10", virtualbox__intnet: true
    # sync ansible folder
    ansible.vm.synced_folder "ansible", "/etc/ansible", create: true

    ansible.vm.provider "virtualbox" do |v|
      v.gui = false
      v.memory = 512
      v.cpus = 1

      # make DNS lookups faster by using host's DNS resolver
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      # use linked clone on newer vagrant
      v.linked_clone = true if Vagrant::VERSION =~ /^1.8/
    end

    ansible.vm.provision "shell", path: "install-ansible.sh"
  end

  config.vm.define 'es' do |es|
    # don't check for box updates (slow)
    es.vm.box_check_update = false
    # specify base box
    es.vm.box = "ubuntu/trusty64"
    # set box hostname
    es.vm.hostname = "es"
    # create private network
    es.vm.network "private_network", ip: "192.168.20.20", virtualbox__intnet: true
    # setup port forwarding
    es.vm.network "forwarded_port", guest: 5601, host: 25601

    es.vm.provider "virtualbox" do |v|
      v.gui = false
      v.memory = 1024
      v.cpus = 1

      # make DNS lookups faster by using host's DNS resolver
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      # use linked clone on newer vagrant
      v.linked_clone = true if Vagrant::VERSION =~ /^1.8/
    end
  end

  config.vm.define 'kibana' do |kibana|
    # don't check for box updates (slow)
    kibana.vm.box_check_update = false
    # specify base box
    kibana.vm.box = "ubuntu/trusty64"
    # set box hostname
    kibana.vm.hostname = "kibana"
    # create private network
    kibana.vm.network "private_network", ip: "192.168.20.30", virtualbox__intnet: true
    # setup port forwarding
    kibana.vm.network "forwarded_port", guest: 5601, host: 35601

    kibana.vm.provider "virtualbox" do |v|
      v.gui = false
      v.memory = 512
      v.cpus = 1

      # make DNS lookups faster by using host's DNS resolver
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      # use linked clone on newer vagrant
      v.linked_clone = true if Vagrant::VERSION =~ /^1.8/
    end
  end
end
