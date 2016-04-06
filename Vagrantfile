Vagrant.configure("2") do |config|
  # ... other stuff

  settings = YAML.load_file '.yml'  

  config.vm.provider :aws do |aws|

    # Access Credentials
    #We could also specify credentials in the ~/.aws/ folder as a profile 
    aws.access_key_id = settings['aws_access_key']
    aws.secret_access_key = settings ['aws_secret_key']

    aws.tags = {
      'Name' => settings['aws_instance_name']
      'Project' => 'vagrant-aws-test'
    }

    # Region Config
    aws.region_config "eu-west-1" do |region|
      # CentOS 7 images
      region.ami = "ami-33734044"
      region.keypair_name = settings['aws_ssh_public_key_name']
    end

    # Storage - $0.125 per GB/month as of April 2016, 100 GB = $12.50 per month
    aws.block_device_mapping = [{
      'DeviceName' => '/dev/sda1',
      'Ebs.VolumeSize' => 100,
      'Ebs.VolumeType' => 'gp2',
      'Ebs.DeleteOnTermination' => 'true' }]

    aws.instance_type = "t2.small" # $14.6 per month as of April 2016

  end
end 
