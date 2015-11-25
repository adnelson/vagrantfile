VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.private_key_path = "/home/anelson/narr/ns_systems/on_prem/dev/vagrant_keys/vagrant"

  config.vm.define :allen do |config|
    config.vm.box = "centos7.1"
    config.ssh.insert_key = false
    config.vm.hostname = "allen.local"
    config.vm.network :private_network, type: "dhcp"
  end

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    v.cpus = 4
    v.memory = 4096
  end

  config.vm.provision "shell" do |s|
    s.inline = "sudo yum install -y epel-release && sudo yum install -y ansible"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.yaml"
    ansible.extra_vars = {
      ns_github_token: ENV['NS_GITHUB_TOKEN']
    }
  end
end
# Have a nice day
