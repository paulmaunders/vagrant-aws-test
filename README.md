## Setup ##
Install the [vagrant-aws plugin](https://github.com/mitchellh/vagrant-aws)
```
vagrant plugin install vagrant-aws
```
Setup your aws credentials in settings.yml (see configuration options below)
```
cp settings.yml.example settings.yml
vim settings.yml
```
Add a dummy box (this won't be used but is necessary to stop errors parsing the Vagrantfile)
```
vagrant box add dummy https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box
```
Launch vagrant
```
vagrant up
```
SSH into the server
```
vagrant ssh
```
## Configuration Options ##
The options you can configure in settings.yml are as follows.

    aws_access_key: "changeme"

Your AWS access key

    aws_secret_key: "changeme"
    
Your AWS secret key

    aws_instance_name: "changeme"
    
A unique name that you wish to give the instance so that you can identify it easily in the AWS EC2 control panel.

    aws_ssh_public_key_name: "changeme"
    
The name of your public key as uploaded to AWS EC2

    aws_subnet_id: "subnet-changeme"
    
The VPC subnet id that you wish to launch the instance into e.g. subnet-123456

    aws_security_group: "sg-changeme"
    
The security group you wish to assign to the instance e.g. sg-123456 - this must be present in the same VPC as the subnet used previously. 

    aws_region: "eu-west-1"
    
The region you wish to launch the instance in. This must contain the VPC subnet chosen previously.

    aws_instance_type: "t2.small"
    
The instance type you wish to use. t2.small costs $14.6 per month as of April 2016

    aws_ami: "ami-33734044"
    
The id of the Amazon Machine Image you want to use, defaults to Centos 7

    aws_instance_username: "centos"
    
The username required to connect to the instance via SSH

    aws_storage_size: 100

The size of the root disk storage in GB. We default to using GP2 SSD storage.

    config_ssh_private_key_path: "~/.ssh/id_rsa.pub"
    
The local path to the SSH private key that corresponds to the public key uploaded to Amazon EC2.
## Debugging errors ##
If you have any difficulties with the above commands, you should enable debugging to get more information from Vagrant.
```
export VAGRANT_LOG=debug
```
