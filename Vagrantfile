ENV["VAGRANT_NO_PARALLEL"] = "yes"
Vagrant.configure("2") do |config|
  N = 3
  (1..N).each do |id|
    config.vm.define "server#{id}" do |server|
      server.vm.box =  "bento/ubuntu-18.04"
      server.vm.provider "parallels" do |prl|
        prl.cpus = 1
        prl.memory = 1024
      end
      server.vm.hostname = "server#{id}"
      server.vm.provision "ansible" do |iac|
        iac.become = true
        iac.playbook = "main.yml"
      end
    end
  end
end