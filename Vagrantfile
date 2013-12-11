# -*- mode: ruby -*-
# # vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "coreos"
  config.vm.box_url = "http://storage.core-os.net/coreos/amd64-generic/dev-channel/coreos_production_vagrant.box"

  # Fix docker not being able to resolve private registry in VirtualBox
  config.vm.provider :virtualbox do |vb, override|
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  docker_systemd_url = "https://gist.github.com/ksikka/7920303/raw/a58ef43700978e9f8f89f3f5fde042be43b7d593/docker-local.service"
  build_script = "curl --silent #{docker_systemd_url} > /media/state/units/docker-local.service"
  build_script += " && /usr/bin/systemctl daemon-reload"
  build_script += " && /usr/bin/systemctl restart local-enable.service"
  build_script += " && /usr/bin/systemctl daemon-reload"

  config.vm.provision "shell", inline: build_script
end
