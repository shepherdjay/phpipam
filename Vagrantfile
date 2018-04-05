Vagrant.configure("2") do |config|
  config.vm.box_download_insecure = true
  config.vm.box = "dharmab/centos7"

  # Share the Ansible playbook for self-provisioning
  config.vm.synced_folder "ansible/", "/ansible/", owner: "root",
    group: "root", mount_options: ["dmode=755", "fmode=644"]

  # Forward port 80 to localhost
  config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Setup Yum
  config.vm.provision "shell", inline: "yum -y update"

  # Script which bootstraps Ansible
  config.vm.provision "shell", path: "ansible/bootstrap.sh", run: "always"
end