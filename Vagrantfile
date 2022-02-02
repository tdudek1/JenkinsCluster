Vagrant.configure("2") do |config|

 config.hostmanager.enabled = true
 config.hostmanager.manage_guest  = true 
 config.vm.synced_folder ".", "/vagrant"
 
 config.vm.define "jenkins" do |jenkins|
   jenkins.vm.box = "generic/centos7"
   jenkins.vm.network "forwarded_port", guest: 8080, host: 8080
   jenkins.vm.hostname = "jenkins.home"
   jenkins.vm.network "private_network",ip: "10.0.1.10" 

   jenkins.vm.provision 'ansible_local', run: 'always', type: :ansible_local do |ansible| 
    ansible.playbook = "jenkins.yaml"
    ansible.become = true
    #ansible.verbose = true
    ansible.galaxy_roles_path = "/etc/ansible/roles"   
    ansible.galaxy_role_file = "requirements.yml" 
    ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force" 
  end
 end

 
  
  (0..1).each do |i|
    config.vm.define "jenkinsagent#{i}" do |jenkinsagent|
      jenkinsagent.vm.box = "generic/centos7"
      jenkinsagent.vm.hostname = "jenkinsagent#{i}.home" 
  
      jenkinsagent.vm.network "private_network", ip: "10.0.1.2#{i}"


      jenkinsagent.vm.provision 'ansible_local', run: 'always', type: :ansible_local do |ansible| 
        ansible.playbook = "jenkinsagent.yaml"
        ansible.become = true
        ansible.verbose = true
        ansible.galaxy_roles_path = "/etc/ansible/roles"   
        ansible.galaxy_role_file = "requirements.yml" 
        ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force" 
      end
    end
  end

end
