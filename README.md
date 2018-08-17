# DigitalOcean Role for Ansible to assign Floating IP to droplets
------------
This role assign an existing [DigitalOcean][digitalocean] Floating IP to an exisisting droplet making use of the DigitalOcean API.

## Role Variables
------------
#### [`digital_ocean_api_token`][digital_ocean_api_token]
Default: `[enc_do_v2_api_key]`

The API key as shown in the DigitalOcean's API Settings.
To be retrieved from DigitalOcean portal.

To be stored in an Ansible Vault. It's very high-sensitivity Information.

#### [`digital_ocean_api_base_url`][digital_ocean_api_base_url]
Default: `'https://api.digitalocean.com/v2/floating_ips/'`

#### [`digital_ocean_droplet_id`][digital_ocean_droplet_id]
Default: `{{ do.droplet.id }}`

#### [`digital_ocean_floating_ip`][digital_ocean_floating_ip]
Default: `none`
This is a mandatory variable and is supposed to be set in the host_vars file for the specific host you want to assign the Floating IP to (because a Floating IP can be associated to only one host at time), in this way you can associate multiple Floating IP to distinct Droplets.

#### [`digital_ocean_static_id`][digital_ocean_static_id]
Default: `{{ ansible_host | mandatory }}`
This paramater is necessary and mandatory to be able to set up the proper IPTABLES postrouting statments to SMTP traffic

#### [`digital_ocean_smtp_ports`][digital_ocean_smtp_ports]
Default: `["25","465","587","2525","2526"]`
This paramater is necessary and mandatory to be able to set up the proper IPTABLES postrouting statments to SMTP traffic

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
[digital_ocean_api_base_url]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L2 "Link to variable on master"
[digital_ocean_api_token]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L3 "Link to variable on master"
[digital_ocean_droplet_id]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L4 "Link to variable on master"
[digital_ocean_floating_ip]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L5 "Link to variable on master"
[digital_ocean_static_id]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L6 "Link to variable on master"
[digital_ocean_smtp_ports]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L7 "Link to variable on master"
[licence]: https://raw.githubusercontent.com/inviqa/ansible-digitalocean-floating-ip/master/LICENSE
