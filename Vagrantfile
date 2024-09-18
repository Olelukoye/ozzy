Vagrant.require_version ">= 2.0.0"

$vm_gui ||= false
$vm_memory ||= 2048
$vm_cpus ||= 2
$ubu1_ip = "192.168.56.10"
$ubu2_ip = "192.168.56.12"
$kibana_ip = $ubu2_ip
$db_user = "root"
$db_password = "new_secure_password"
$elk_version = "7"

Vagrant.configure("2") do |config|

    config.vm.define "ubu1" do |ubu1|
      ubu1.vm.hostname = "ubu1"
      ubu1.vm.box = "generic/ubuntu2204"
      ubu1.vm.network "private_network", ip: $ubu1_ip
      ubu1.vm.network "forwarded_port", guest: 80, host: 8080
      ubu1.vm.provider :virtualbox do |vb|
        vb.gui = $vm_gui
        vb.memory = $vm_memory
        vb.cpus = $vm_cpus
      end
      ubu1.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbooks/lemp.yml"
        ansible.groups = {
          "lemp" => ["ubu1"],
          "all" => ["ubu1"]
        }
        ansible.become = true
        ansible.limit = "all,localhost"
        ansible.compatibility_mode = "2.0"
        ansible.extra_vars = {
          "kibana_ip" => $kibana_ip,
          "db_user" => $db_user,
          "db_password" => $db_password,
          "elk_version" => $elk_version
        }
      end
    end
  
    config.vm.define "ubu2" do |ubu2|
      ubu2.vm.hostname = "ubu2"
      ubu2.vm.box = "generic/ubuntu2204"
      ubu2.vm.network "private_network", ip: $ubu2_ip
      ubu2.vm.network "forwarded_port", guest: 5601, host: 5601
      ubu2.vm.provider :virtualbox do |vb|
        vb.gui = $vm_gui
        vb.memory = $vm_memory
        vb.cpus = $vm_cpus
      end
      ubu2.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbooks/elk.yml"
        ansible.groups = {
          "elk" => ["ubu2"],
          "all" => ["ubu2"]
        }
        ansible.become = true
        ansible.limit = "all,localhost"
        ansible.compatibility_mode = "2.0"
        ansible.extra_vars = {
          "kibana_ip" => $kibana_ip,
          "elk_version" => $elk_version
        }
      end
    end
  end
  