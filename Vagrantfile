Vagrant.configure("2") do |config|
  # ... other stuff
  
  config.vm.box = "dummy"
 
  settings = YAML.load_file 'settings.yml'  

  config.vm.provider :aws do |aws|

    # Access Credentials
    #We could also specify credentials in the ~/.aws/ folder as a profile 
    aws.access_key_id = settings['aws_access_key']
    aws.secret_access_key = settings ['aws_secret_key']

    aws.tags = {
      'Name' => settings['aws_instance_name'],
      'Project' => 'vagrant-aws-test'
    }
    
    aws.instance_type = settings['aws_instance_type'] # $14.6 per month as of April 2016
    aws.ami = settings['aws_ami']
    aws.keypair_name = settings['aws_ssh_public_key_name']
    aws.region = settings['aws_region']
    aws.subnet_id = settings['aws_subnet_id']
    aws.security_groups = [settings['aws_security_group']]
    aws.associate_public_ip = true

    # Storage - $0.125 per GB/month as of April 2016, 100 GB = $12.50 per month
    aws.block_device_mapping = [{
      'DeviceName' => '/dev/sda1',
      'Ebs.VolumeSize' => settings['aws_storage_size'],
      'Ebs.VolumeType' => 'gp2',
      'Ebs.DeleteOnTermination' => 'true' }]

    # Override default Vagrant ssh keys
    config.ssh.username = settings['aws_instance_username']
    config.ssh.private_key_path = settings['config_ssh_private_key_path']

  end

  config.vm.define "origin" do |org|

    org.vm.hostname = "origin"

    org.vm.provision "ansible" do |ansible|
      ansible.playbook = "site.yml"
      ansible.verbose = "vvvv"
    end

  end

end 
