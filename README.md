# DigitalOcean Role for Ansible to assign Floating IP to droplets
------------
This role assign an existing [DigitalOcean][digitalocean] Floating IP to an exisisting droplet making use of the DigitalOcean API.

It also sets up IPTABLES to:
- route all traffic through Digital Ocean Anchor IP
- route all SMTP traffic through the Droplet static IP

The IPTABLES will be by default set up via the `geerlingguy.firewall` Galaxy role.
You will need to add such `firewall` role to your playbook, which will grant that the IPTABLES rules will be persistent through the lifecycle of your droplet.

In case you do not want to make use of the `geerlingguy.firewall` Galaxy role you can disable it setting to false:
```
digital_ocean_use_firewall: false
```
With that the IPTALES will be set as raw IPTABLES via Ansible's core `iptables` module, BUT THEY WONT ?BE PERSISTENT through the Droplet lifecycle (i.e. if the Droplet is restarted you will lose the IPTABLAES rules)

## Role Variables
------------

#### [`digital_ocean_api_base_url`][digital_ocean_api_base_url]
Default: `'https://api.digitalocean.com/v2/floating_ips/'`

#### [`digital_ocean_metadata_anchor_ipv4_url`][digital_ocean_metadata_anchor_ipv4_url]
Default:`'http://169.254.169.254/metadata/v1/interfaces/public/0/anchor_ipv4/address'`

#### [`digital_ocean_api_token`][digital_ocean_api_token]
Default: `[enc_do_v2_api_key]`

The API key as shown in the DigitalOcean's API Settings.
To be retrieved from DigitalOcean portal.

To be stored in an Ansible Vault. It's very high-sensitivity Information.
#### [`digital_ocean_droplet_id`][digital_ocean_droplet_id]
Default: `{{ do.droplet.id }}`

#### [`digital_ocean_floating_ip`][digital_ocean_floating_ip]
Default: `none`
This is a mandatory variable and is supposed to be set in the host_vars file for the specific host you want to assign the Floating IP to (because a Floating IP can be associated to only one host at time), in this way you can associate multiple Floating IP to distinct Droplets.

#### [`digital_ocean_smtp_ports`][digital_ocean_smtp_ports]
Default: `["25","465","587","2525","2526"]`
This parameter is necessary and mandatory to be able to set up the proper IPTABLES postrouting statments to SMTP traffic

#### [`digital_ocean_iptables_temp_file`][digital_ocean_iptables_temp_file]
Default: `"/tmp/iptables.save"`
This parameter is necessary and mandatory in the process to temporarely disable the IPTABLES to obatin the DO Anchor IP and also during the testing process

#### [`digital_ocean_use_firewall`][digital_ocean_use_firewall]
Default: `true`
This parameter is necessary and mandatory to define how the IPTABLES will be used: via a firewall role or via raw IPTABLES

## Example Playbook
----------------

```YAML
---
- hosts: production
  roles:
     - { role: inviqa.digitalocean-floating-ip, digital_ocean_api_token: 'abcdef012234343' }

- hosts: specific_host_name
  vars:
    digital_ocean_floating_ip: "123.456.678.90"
...
```
## TODO

## License
-------

[MIT][licence]

## Author Information
------------------
Author Marco Massari Calderone at Inviqa UK Ltd

[github]: https://github.com/inviqa/ansible-digitalocean-floating-ip "Github location of this role"
[digitalocean]: https://digitalocean.com "DigitalOcean website"
[digital_ocean_api_base_url]:
https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L2 "Link to variable on master"
[digital_ocean_metadata_anchor_ipv4_url]:
https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L3 "Link to variable on master"
[digital_ocean_api_token]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L4 "Link to variable on master"
[digital_ocean_droplet_id]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L5 "Link to variable on master"
[digital_ocean_floating_ip]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L6 "Link to variable on master"
[digital_ocean_smtp_ports]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L7 "Link to variable on master"
[digital_ocean_iptables_temp_file]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L8 "Link to variable on master"
[digital_ocean_use_firewall]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L9 "Link to variable on master"
[licence]: https://raw.githubusercontent.com/inviqa/ansible-digitalocean-floating-ip/master/LICENSE
