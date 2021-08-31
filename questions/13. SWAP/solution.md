# 13. SWAP - Solution

The playbook might look as follows
```yml
---
- name: Configure SWAP
  hosts: database
  become: true
  gather_facts: false
  vars:
    vg: swap
    lv: swap
  tasks:
  - name: Install tools
    yum:
      name: lvm2
  - name: Partition the drive
    parted:
      device: /dev/sdb
      label: gpt
      number: 1
      state: present
      part_start: 0%
      part_end: 1100MB
  - name: Create volume group
    lvg:
      pvs: /dev/sdb1
      vg: "{{ vg }}"
  - name: Create logical volume
    lvol:
      lv: "{{ lv }}"
      size: 100%VG
      vg: "{{ vg }}"
  - name: Create filesystem
    filesystem:
      dev: /dev/{{ vg }}/{{ lv }}
      fstype: swap
  - name: Mount on boot
    lineinfile:
      line: "/dev/{{ vg }}/{{ lv }} swap swap defaults 0 0"
      path: /etc/fstab
  - name: Check if mounted
    shell: "lsblk -s | grep {{ vg }}-{{ lv }}"
    changed_when: false
    register: mounts
  - name: Mount if not mounted
    shell: swapon /dev/{{ vg }}/{{ lv }}
    when: "'[SWAP]' not in mounts.stdout"
...
```

In order to execute the playbook run 
```bash
ansible-playbook swap.yml
```

#### Readers note
I couldn't use `mount` module due to [this bug](https://github.com/ansible/ansible/issues/29647)