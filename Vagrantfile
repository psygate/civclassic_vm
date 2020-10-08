Vagrant.require_version ">= 1.8.0"

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"
    config.vm.define "civmaster" do |civmaster|
        civmaster.vm.network "private_network", ip: "172.20.21.22"
        civmaster.vm.network "public_network"
        civmaster.vm.hostname = "civmaster"

        civmaster.vm.provider "virtualbox" do |v|
            v.gui = false
            v.memory = 2048
            v.cpus = 2
        end

        civmaster.vm.provision "ansible_local" do |ansible|
            ansible.install = true
            ansible.verbose = "v"
            ansible.limit = "all"
            ansible.playbook = "provisioning/ansible/playbooks/civ_civserver_setup.yml"
            ansible.inventory_path = "provisioning/ansible/inventory.yml"
        end

        civmaster.vm.provision "ansible_local" do |ansible|
            ansible.install = true
            ansible.verbose = "v"
            ansible.limit = "civmaster"
            ansible.playbook = "provisioning/ansible/playbooks/civ_civmaster_setup.yml"
            ansible.inventory_path = "provisioning/ansible/inventory.yml"
        end

        civmaster.vm.provision "ansible_local" do |ansible|
            ansible.install = true
            ansible.verbose = "v"
            ansible.limit = "civmaster"
            ansible.playbook = "provisioning/ansible/playbooks/civ_civmaster_project_setup.yml"
            ansible.inventory_path = "provisioning/ansible/inventory.yml"
        end

        config.trigger.after :provision do |trigger|
          trigger.info = "Bringing up shared folders."
          civmaster.vm.synced_folder "projects/", "/home/mc/projects/", owner: "mc", group: "mc", automount: true
          civmaster.vm.synced_folder "master_server/", "/home/mc/server/", owner: "mc", group: "mc", automount: true
        end
    end
end