# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version ">= 1.6.0"
# Vagrant::DEFAULT_SERVER_URL.replace('https://vagrantcloud.com')

# settings
$name = "local-wp-ansible"
$addr = "192.168.33.10"
$playbook = "./ansible/localhost.yml"
$ansible_dir = "./ansible"
$wp_dir = "wordpress"
$inventory = "hosts"
$playbook = "localhost.yml"

Vagrant.configure(2) do |config|
  config.vm.box = "centos/7"
  config.vm.box_check_update = false
  config.vbguest.auto_update = false
  config.ssh.forward_agent = true

  config.vm.define $name do |conf|
    conf.vm.hostname = $name
    conf.vm.network "private_network", ip: $addr
    conf.vm.synced_folder $ansible_dir, "/home/vagrant/ansible"
    # conf.vm.synced_folder $wp_dir, "/home/vagrant/wordpress",:owner=> 'vagrant', :group=>'apache', :mount_options => ['dmode=775', 'fmode=775']
    conf.vm.synced_folder $wp_dir, "/home/vagrant/wordpress"
    conf.vm.provision :shell, :privileged => false, :inline => <<-EOT
        which ansible >/dev/null 2>&1 || {
          sudo yum install -y epel-release
          sudo yum --enablerepo=epel install -y ansible
        }
        ansible-playbook -i ansible/#{$inventory} -c local ansible/#{$playbook}
      EOT
  end
end
