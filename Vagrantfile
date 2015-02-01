# Require YAML module
require 'yaml'
 
# Read YAML file with box details
aws_config = YAML.load_file(File.expand_path("~") + "/" + ".vagrant-aws")

Vagrant.configure("2") do |config|
  config.vm.box = "dummy"

  config.vm.provider :aws do |aws, override|

    # Load from config file
    aws.access_key_id = aws_config["access_key_id"]
    aws.secret_access_key = aws_config["secret_access_key"]
    aws.keypair_name = aws_config["keypair_name"]

    # Customizations
    aws.region = "us-west-2"
    aws.associate_public_ip = true
    aws.security_groups = ["sg-4ed6cb22", "sg-ac4b0dc9", "sg-a11343c4"]
    aws.subnet_id = "subnet-65c6780c"
    aws.tags = {
      "Name" => "Vagrant Dummy Box",
      "Stack" => "test"
    }
    aws.ami = "ami-3d50120d" # Ubuntu Server 14.04 LTS (HVM), SSD Volume Type
    aws.instance_type = "t2.small"
    #aws.iam_instance_profile_name = "VagrantRole"

    # Override config above with anything specified in config file
    aws_config.each do |key, value|
      aws.send("#{key}=",value)
    end

    override.ssh.username = "ubuntu"
    override.ssh.private_key_path = File.expand_path("~") + "/.ssh/id_rsa"
  end


  # Disable sync folder
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # Install stuff
  config.vm.provision "shell", inline: "sudo apt-get install -y mosh git fish"
  config.vm.provision "shell", inline: "git clone https://github.com/joech4n/zsh-dotfiles.git ~/.dotfiles && ~/.dotfiles/script/bootstrap -n", privileged: false

=begin
  config.vm.provision "chef_solo" do |chef|
    chef.add_recipe "apache2"
  end
=end

end
