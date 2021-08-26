# 14. System target

Create a playbook that meets following requirements:
* Is placed at `/home/automation/plays/system_target.yml`
* Runs against all managed hosts
* Sets target to `multi-user.target`
* Must be idempotent - subsequent execution of playbook shouldn't result in `changed` state