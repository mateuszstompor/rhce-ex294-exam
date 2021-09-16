# 22. Extending facts

Write a playbook named `additional_facts.yml` that meets following requirements:
* Is placed at `/home/automation/plays`
* Gathers facts about all hosts
* Gets data related to installed packages on `database` belonging hosts
* Prints facts of each host to the console