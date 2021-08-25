# 13. SWAP

Create a playbook that meets following requirements:
* Is placed at `/home/automation/plays/swap.yml`
* Runs against `database` group
* Creates a partition on sdb drive on the managed hosts of size between 1000MB-1100MB
* Uses this partition to extend available swap
* Ensures that the partition is part of the swap pool on boot