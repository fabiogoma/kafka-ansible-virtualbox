zookeeper_boxes = %w(zookeeper1 zookeeper2 zookeeper3)
kafka_boxes = %w(kafka1 kafka2 kafka3)

Vagrant.configure('2') do |config|
  config.vm.box = 'centos/7'
  # config.vm.box_version = '1703.01'
  config.vm.network 'private_network', :type => 'dhcp', :name => 'vboxnet0', :adapter => 2
  config.vm.synced_folder '.', '/vagrant', disabled: true
  config.vm.provider 'virtualbox' do |vb|
    vb.memory = '2048'
  end

  zookeeper_boxes.each_with_index do |box, index|
    config.vm.define box.to_s do |node|
      node.vm.hostname = box.to_s
      node.vm.provision 'ansible' do |ansible|
        ansible.limit = box.to_s
        ansible.verbose = false
        ansible.extra_vars = { 'zookeeper_server_list' => zookeeper_boxes, 'server_id' => index }
        ansible.playbook = 'provisioning/zookeeper-playbook.yml'
      end
    end
  end

  kafka_boxes.each_with_index do |box, index|
    config.vm.define box.to_s do |node|
      node.vm.hostname = box.to_s
      node.vm.provision 'ansible' do |ansible|
        ansible.limit = box.to_s
        ansible.verbose = false
        ansible.extra_vars = { 'zookeeper_server_list' => zookeeper_boxes, 'server_id' => index }
        ansible.playbook = 'provisioning/kafka-playbook.yml'
      end
    end
  end

end 
