# 16. Roles

1. Create a role called `apache` that meets following requirements:
* Is placed at `/home/automation/plays/roles/apache`
* Installs `httpd` and `firewalld` packages
* Allows ports 80 and 443 to be accessible through firewall
* Ensures that httpd and firewalld services are started at boot time
* Deploys an index page that presents following message: `Welcome, you have conntected to <fqdn>`

2. Create a playbook that meets following requirements:
* Is placed at `/home/automation/plays/apache.yml`
* Runs role apache against `webservers` hosts group