# Vagrant Base Box
### CentOS 7 with Python3.6.3 and Guest Additions 5.1.26

---

#### Usage
To use it, simply:

* Install [packer](https://www.packer.io/)
* Set the following environment variables with your Vagrant Cloud credentials:
  * ```export VAGRANT_ACCESS_TOKEN=<Your Vagrant Cloud access token>```
  * ```export VAGRANT_BOX_TAG=<Your Vagrant Cloud username/box_name>```
* Run: ```packer build packer_template.json```
* For more info or to contribute, see the [github page](https://github.com/rollerd/vagrant_centos7py36)


#### Customizing

This Packer template uses a combination of a basic kickstart script and a few [Ansible](https://www.ansible.com/) roles to build out the base box from a starting CentOS7 iso. All of this can be changed by editing the following files:

* To change base iso image, edit the `packer_template.json` file, and edit the "iso_url" and "iso_checksum" options under "builders"
* To change the Python version that gets installed, edit the `roles/python_install/defaults/main.yml` file and edit each option to reflect the Python version you'd like to use
* Any additional system packages that you would like to install can be added in the `roles/prep_base_image/defaults/main.yml` file "required_packages" list

##### NOTE: 
#### The GuestAdditions version that gets installed will be dictated by the version of Virtualbox on the system doing the Packer build by default. You would need to create a new role to install a version of GuestAdditions different from that if you needed such a thing

