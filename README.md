# Vagrant Base Box
### CentOS 7 with Python3.6.4 and Guest Additions 5.2.4

---
#### What it is
This repo contains the Packer, kickstart, and Ansible scripts to create a CentOS7 Vagrant box with Python36 and Virtualbox Guest Additions installed on it.

Python3.6 is installed alongside the system Python(2.7.5) and the user's PATH is set so that 3.6 is the 'active' version by default. The box is built from the CentOS7 minimal iso with additional packages installed as needed for some of the most common uses in Python. All of this can be customized (see below), but if you use this base box by pulling from my [Vagrant Cloud](https://app.vagrantup.com/rollerd/boxes/centos7py36) and find there is a common package missing or some other bug, please feel free to put in a pull request or open an issue.

Thanks for taking a look, I hope this is useful!

#### Usage
To use it, simply create a Vagrantfile with the following: 
```
Vagrant.configure("2") do |config|
  config.vm.box = "rollerd/centos7py36"
end
```

OR, to create your own base box from this template:

* Install [packer](https://www.packer.io/)
* Run: ```packer build packer_template.json```
* For more info or to contribute, see the [github page](https://github.com/rollerd/vagrant_centos7py36)


#### Customizing

This Packer template uses a combination of a basic kickstart script and a few [Ansible](https://www.ansible.com/) roles to build out the base box from a starting CentOS7 iso. All of this can be changed by editing the following files:

* To change base iso image, edit the `packer_template.json` file, and edit the "iso_url" and "iso_checksum" options under "builders"
* To change the Python version that gets installed, edit the `roles/python_install/defaults/main.yml` file and edit each option to reflect the Python version you'd like to use
* Any additional system packages that you would like to install can be added in the `roles/prep_base_image/defaults/main.yml` file "required_packages" list

##### NOTE: 
#### The GuestAdditions version that gets installed will be dictated by the version of Virtualbox on the system doing the Packer build by default. You would need to create a new role to install a version of GuestAdditions different from that if you needed such a thing

