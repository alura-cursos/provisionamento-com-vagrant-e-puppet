Vagrant.configure("2") do |config|

	config.vm.box = "hashicorp/precise32"
	# config.vm.box = "ubuntu_awss"
	# config.vm.box_url = "https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box"

	config.vm.provider :aws do |aws, override|
	    aws.access_key_id = "AKIAIF5E4LTI53TXUWZA"
	    aws.secret_access_key = "6QEsL4F+DqngbvD7uWvZWBB18sDCEKw9Fdasm2un"

		aws.keypair_name = "palestra-devops"
		aws.ami = "ami-358c955c"
		aws.security_groups = ['devops-vagrant']

		override.ssh.username = "ubuntu"
		override.ssh.private_key_path = "palestra-devops.pem"
	end

	config.vm.define :web do |web_config|
		web_config.vm.network "private_network", ip: "192.168.50.10"
		web_config.vm.provision "shell", path: "manifests/bootstrap.sh"
		web_config.vm.provision "puppet" do |puppet|
			puppet.manifest_file = "web.pp"
		end
		web_config.vm.provider :aws do |aws|
			aws.tags = { 'Name' => 'MusicJungle (vagrant)'}
		end
	end

end