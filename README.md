## Setup ##
Install the vagrant-aws plugin
```
vagrant plugin install vagrant-aws
```
Setup your aws credentials in settings.yml
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
