Vagrant.configure("2") do |config|

  config.hostmanager.enabled = true
  config.hostmanager.manage_guest  = true
  
  config.vm.define "jenkins" do |jenkins|
    jenkins.vm.box = "generic/centos8"
    jenkins.vm.network "forwarded_port", guest: 8080, host: 8080
    jenkins.vm.hostname = "jenkins.home"
    jenkins.vm.network "private_network",ip: "192.168.56.10" 

    jenkins.vm.provision 'ansible', run: 'always', type: :ansible do |ansible| 
      ansible.playbook = "jenkins.yml"
      ansible.become = true
    end
  end

 
  config.vm.define "jenkinsagent" do |jenkinsagent|
      jenkinsagent.vm.box = "generic/centos8"
      jenkinsagent.vm.hostname = "jagentlinux.home"   
      jenkinsagent.vm.network "private_network", ip: "192.168.56.20"

      jenkinsagent.vm.provision 'ansible', run: 'always', type: :ansible do |ansible| 
        ansible.playbook = "jenkinsagent.yml"
        ansible.become = true
      end
  end


  config.vm.define "jenkinsagentwindows" do |jenkinsagentwindows|   
    jenkinsagentwindows.vm.box = "gusztavvargadr/windows-server"
    jenkinsagentwindows.vm.hostname = "jagentwindows" 
    jenkinsagentwindows.vm.network "private_network", ip: "192.168.56.30"

    jenkinsagentwindows.vm.provision 'ansible', run: 'always', type: :ansible do |ansible| 
          ansible.playbook = "jenkinsagentwindows.yml"
          ansible.become_user = "Administrator"
          ansible.raw_arguments = ["-e","ansible_winrm_scheme=http"]
    end
  end

end
