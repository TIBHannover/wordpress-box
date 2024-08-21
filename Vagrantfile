#require 'yaml'
#settings = YAML.load_file 'ansible/group_vars/all.yml'

Vagrant.configure("2") do |config|

  config.vm.define "wordpress-vm" do |srv|
    srv.vm.box = "debian/bookworm64"
    srv.ssh.insert_key = false
    srv.vm.hostname = "wordpress.box"
    srv.vm.network :private_network, ip: "192.168.98.117"

    srv.vm.provider :virtualbox do |vb|
      vb.name = "wordpress"
      vb.memory = 4048
      vb.cpus = 2
    end
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.install = true
    ansible.compatibility_mode = "2.0"
    ansible.install_mode = "pip"
    ansible.pip_install_cmd = "sudo apt update && sudo apt install python3-pip -y"
    ansible.pip_args = "ansible-core==2.16.10 --break-system-packages"
    ansible.playbook = "ansible/playbook.yml"
    ansible.galaxy_role_file = "requirements.yml"
    ansible.verbose = "true"
  end
  
end
