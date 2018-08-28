
# Multi-Platform Ansible Role and Playbook Test VMs

Use Digital Ocean to provision a set of Droplets to which associate Floating IPs created on the run, and this project runs a playbook against the following OSes:

  - Debian Stable
  - Ubuntu 14.04.x
  - Ubuntu 16.04.x
  - CentOS 6.x (192.168.3.6)
  - CentOS 7.x (192.168.3.5)

## Requirements

set local Environment Variables that will be read by Ansible
```
DIGITAL_OCEAN_API_TOKEN=xxxxxxxxxxxxxyyyyyyyyyyyyyyzzzzzzzzzz
# The SSH Key ID available in DO which will have access and provision the droplets
DIGITAL_OCEAN_SSH_KEY_ID=yyyyyyyyyyyyyyzzzzzzzzzzxxxxxxxxxxxxx
```

## Testing a Role
The testing process works as follows:
There are an Ansible Playbook and Inventory configured to spin a bunch of Digital Ocean droplets.
Ansible will install associate to these Droplets newly created Floating IPs.

At the end of the provisioning Ansible will run a few test-tasks that will verify if the Floating IPs have been generated and associated correctly each one to a different Droplet, including an idempotence test (the privisioning will be run twice on the same containers without rebuilding or restarting them)

This is the command to start the testing process

```
ansible-playbook -i inventory playbook.yml
```

To run the test on a specific containers you will need to create additional inventory files, i.e:


```
# *inventory-centos*

[centos]
centos7 do_image_id=centos-7-x64
centos6 do_image_id=centos-6-x64

[digital-ocean:children]
centos


```

This command is to to run a playbook which will instruct DigitalOcean to destroy the droplets and the associated Floating IPs.
```
cd  ./tests
ansible-playbook -i inventory playbook_cleanup.yml

```

### Travis CI Testing
For the testing to work set up in the Travis CI project's settings the following `Environment Variables` that will be read by Ansible

```
DIGITAL_OCEAN_API_TOKEN=yyyyyyyyyyyyyyzzzzzzzzzzxxxxxxxxxxxxx
# The SSH Key ID available in DO which will have access and provision the droplets
DIGITAL_OCEAN_SSH_KEY_ID=yyyyyyyyyyyyyyzzzzzzzzzzxxxxxxxxxxxxx
```

## License

MIT

## Author Information

Created in 2014 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
