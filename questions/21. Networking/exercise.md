# 21. Networking

Create a playbook named `network.yml` at `/home/automation/plays` that configures eth2 interface on **managed1.example.com** and **managed4.example.com**

Meet following objectives:
* It defines new connection named `Internal`
* Addresses for hosts are defined as below, each having 24-bit mask 
    * `192.168.57.101` - managed1.example.com
    * `192.168.57.104` - managed4.example.com 
* Connection should be up on boot
* Type of the connection is set to ethernet
* Uses system role for it
