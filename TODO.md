- [ ] improve the Check if DO Floating IP exists to actualy check if the
FloatingIP exists
- [ ] make the digital_ocean_floating_ip attribute not mandatory
- [ ] if a floating IP is not specifified implement a task to generate a FloatingIP on-the-fly and assign it directly to the droplet
- [ ] create a task to delete a floating IP (to be used to remove the FloatingIPs generated on-the-fly)
- [ ] make use of the `firewall` role to apply the required IPTABLES rules
- [ ] add TrevisCI integration
