Vagrant.configure("2") do |config|
  if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.http     = "http://10.0.2.2:10809/"
    config.proxy.https    = "http://10.0.2.2:10809/"
    config.proxy.no_proxy = "localhost,127.0.0.1"
  end

  hostname = File.basename(Dir.getwd)
  config.vm.define "#{hostname}" do |app|
    app.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "4096"
      vb.cpus = 4
    end
    app.vm.hostname = "#{hostname}"
    app.vm.box = "bento/ubuntu-18.04"
    app.vm.box_check_update = false
    app.ssh.insert_key = false
    app.ssh.private_key_path = ['~/.vagrant.d/insecure_private_key']
    app.vm.network "private_network", ip: "10.18.18.18"
    app.vm.network "public_network"
    app.vm.provision "shell", path: "prepare.sh"
  end
end
