# 5. Ansible Facts

* Create a playbook that meets following requirements:
    * Is placed at `/home/automation/plays/ansible_facts.yml` 
    * Runs against `proxy` group
    * Results in possiblity of getting a pair `name=haproxy` from ansible facts path `ansible_local.environment.application` after calling setup module
