# -*- mode: ruby -*-
def utop_autocomplete_config(machine)
  machine.vm.provision "file", source: "vagrant.d/.lambda-term-inputrc", destination: "$HOME/.lambda-term-inputrc"
end

def ssh_key_permissions(machine)
  machine.vm.provision "shell", inline: "chmod u+w $HOME/.ssh/authorized_keys"
end

def workaround_monterey_headless_bug
  if Vagrant::Util::Platform.darwin?
    config.vm.provider "virtualbox" do |v|
      v.gui = true
    end
  end
end

Vagrant.configure(2) do |config|
   config.vm.provider "virtualbox" do |vb|
     vb.memory = "2048"
   end
   
   config.vm.define "cs-linux" do |machine|
     machine.vm.box = "Neowizard/cs-linux"
     machine.ssh.insert_key = true
     machine.vm.synced_folder ".", "/home/vagrant/compiler"
     workaround_monterey_headless_bug
     utop_autocomplete_config machine
  end

end
