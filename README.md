# DigitalOcean Role for Ansible to assign Floating IP to droplets
------------
This role assign an existing [DigitalOcean][digitalocean] Floating IP to an exisisting droplet making use of the DigitalOcean API.

## Requirements
------------
[cURL][curl] and NTP should be installed as prerequisites.

## Role Variables
------------
#### [`digital_ocean_api_token`][digital_ocean_api_token]
Default: `[enc_do_v2_api_key]`

The API key as shown in the DigitalOcean's API Settings.
To be retrieved from DigitalOcean portal.

To be stored in an Ansible Vault. It's very high-sensitivity Information.

digital_ocean_droplet_id:         ""
digital_ocean_floating_ip:        ""
#### [`digital_ocean_api_base_url`][digital_ocean_api_base_url]
Default: `'https://api.digitalocean.com/v2/floating_ips/'`

#### [`digital_ocean_droplet_id`][digital_ocean_droplet_id]
Default: `none`
#### [`digital_ocean_floating_ip`][digital_ocean_floating_ip]
Default: `none`
## Example Playbook
----------------

```YAML
---
- hosts: production
  roles:
     - { role: inviqa.digitalocean-floating-ip, digital_ocean_api_token: 'abcdef012234343' }
  vars:
    digital_ocean_droplet_id: "123456790"
    digital_ocean_floating_ip: "123.456.678.90"
...
```
## TODO
- [ implement all the tasks]
- [ ]
- [ ]
- [ ]

## License
-------

[MIT][licence]

## Author Information
------------------
Author Marco Massari Calderone at Inviqa UK Ltd

[github]: https://github.com/inviqa/ansible-digitalocean-floating-ip "Github location of this role"
#[curl]: https://galaxy.ansible.com/list#/roles/4384
[digitalocean]: https://digitalocean.com "DigitalOcean website"
[digital_ocean_api_base_url]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L2 "Link to variable on master"
[digital_ocean_api_token]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L3 "Link to variable on master"
[digital_ocean_droplet_id]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L4 "Link to variable on master"
[digital_ocean_floating_ip]: https://github.com/inviqa/ansible-digitalocean-floating-ip/blob/master/defaults/main.yml#L5 "Link to variable on master"
[licence]: https://raw.githubusercontent.com/inviqa/ansible-digitalocean-floating-ip/master/LICENSE
