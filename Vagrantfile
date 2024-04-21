ENV["LC_ALL"] = "en_US.UTF-8"
ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'

# Описание параметров ВМ
MACHINES = {
  # Имя DV "pam"
  :web => {
        # VM box
#        :box_name => "centos/stream8",
        :box_name => "ubuntu/jammy64",
        # Имя VM
        :vm_name => "web",
        # Количество ядер CPU
        :cpus => 2,
        # Указываем количество ОЗУ (В Мегабайтах)
        :memory => 2048,
        # Указываем IP-адрес для ВМ
        :ip => "192.168.56.10",
  },
  :log => {
    #    :box_name => "centos/stream8",
        :box_name => "ubuntu/jammy64",
        :vm_name => "log",
        :cpus => 2,
        :memory => 2048,
        :ip => "192.168.56.15",

  },
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|
    
    config.vm.define boxname do |box|
   
      box.vm.box = boxconfig[:box_name]
      box.vm.host_name = boxconfig[:vm_name]
      box.vm.network "private_network", ip: boxconfig[:ip]
      box.vm.provider "virtualbox" do |v|
        v.memory = boxconfig[:memory]
        v.cpus = boxconfig[:cpus]
      end

      # Запуск ansible-playbook
      if boxconfig[:vm_name] == "log"
       box.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/provision_log.yml"
        ansible.inventory_path = "ansible/hosts"
        ansible.host_key_checking = "false"
        ansible.limit = "all"
       end
      end

      # Запуск ansible-playbook
      if boxconfig[:vm_name] == "web"
        box.vm.provision "ansible" do |ansible|
         ansible.playbook = "ansible/provision_web.yml"
         ansible.inventory_path = "ansible/hosts"
         ansible.host_key_checking = "false"
         ansible.limit = "all"
        end
       end


    end
  end
end



# ENV["LC_ALL"] = "en_US.UTF-8"
# ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'

# MACHINES = {
#   :"web" => {
#               :box_name => "ubuntu/jammy64",
#               :vm_name => "web",
#               :cpus => 2,
#               :memory => 1512,
#               :ip => "192.168.56.10",
#             },
#   :"log" => {
#               :box_name => "ubuntu/jammy64",
#               :vm_name => "log",
#               :cpus => 2,
#               :memory => 1512,
#               :ip => "192.168.56.15",
#             },
                        
# }

# Vagrant.configure("2") do |config|

#   MACHINES.each do |boxname, boxconfig|

#     config.vm.define boxname do |box|

#       box.vm.box = boxconfig[:box_name]
#       box.vm.host_name = boxconfig[:vm_name]
#       box.vm.network "private_network", ip: boxconfig[:ip]
#       box.vm.provider "virtualbox" do |v|
#         v.memory = boxconfig[:memory]
#         v.cpus = boxconfig[:cpus]
#       end

#       # Запуск ansible-playbook
#       if boxconfig[:vm_name] == "web"
#        box.vm.provision "ansible" do |ansible|
#         ansible.playbook = "ansible/provision_web.yml"
#         ansible.inventory_path = "ansible/hosts"
#         ansible.host_key_checking = "false"
#         ansible.limit = "all"
#       end
#       if boxconfig[:vm_name] == "log"
#         box.vm.provision "ansible" do |ansible|
#          ansible.playbook = "ansible/provision_log.yml"
#          ansible.inventory_path = "ansible/hosts"
#          ansible.host_key_checking = "false"
#          ansible.limit = "all"
#       end
#     end
#     end
#     end
#   end
# end