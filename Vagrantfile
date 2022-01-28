Vagrant.configure("2") do |config|

  config.vm.define "jenkins" do |jenkins|
    jenkins.vm.box = "generic/centos7"
    jenkins.vm.network "forwarded_port", guest: 8080, host: 8080
    jenkins.vm.hostname = "jenkins.home"


    jenkins.vm.provision 'ansible', run: 'always', type: :ansible do |ansible| 
      ansible.playbook = "jenkins.yaml"
    end
  end

  config.vm.define "jenkinsagent" do |jenkinsagent|
    jenkinsagent.vm.box = "generic/centos7"
    jenkinsagent.vm.hostname = "jenkinsagent.home"


    jenkinsagent.vm.provision 'ansible', run: 'always', type: :ansible do |ansible| 
      ansible.playbook = "jenkinsagent.yaml"
    end
  end
end
