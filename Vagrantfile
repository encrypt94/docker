ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'

Vagrant.configure("2") do |config|

  config.vm.define "nerdzeu" do |nerdz|
    nerdz.vm.network "forwarded_port", host: 8080, guest: 80

    nerdz.vm.provider :docker do |docker|
      docker.build_dir = "./vagrant"
      docker.has_ssh = true
    end
  end
end
