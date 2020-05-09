Vagrant.configure("2") do |config|
  ENV['VAGRANT_NO_PARALLEL'] = 'yes'
  N = 3
  (1..N).each do |machine_id|
    config.vm.define "ubuntu#{machine_id}" do |machine|
      machine.vm.box =  "bento/ubuntu-18.04"
      machine.vm.provider "parallels" do |prl|
        prl.cpus = "1"
        prl.memory = "512"
      end
      machine.vm.provision "shell", inline: "apt-add-repository --yes --update ppa:ansible/ansible;apt install ansible -y"
      machine.vm.provision "ansible_local" do |ansible|
        ansible.become = true
        ansible.playbook = "main.yml"
        ansible.galaxy_role_file = "req.yml"
        ansible.galaxy_roles_path = "/etc/ansible/roles"
        ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
      end
    end
  end
end