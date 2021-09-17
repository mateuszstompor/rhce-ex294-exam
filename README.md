# EX294 Exam Preparations
Repository contains exercises preparing for EX294 exam.
It should be treated as a database of questions but the readers need to keep in mind that none of them was taken from the actual test. 
They were created based on the study point available at RedHat's website

## Inspiration
Content present in the repository is inspierd by other people' sample exams, redhat training exercises and my own invention. Use links below to check them out
* [Red Hat Training](https://www.redhat.com/en/services/training/rh294-red-hat-linux-automation-with-ansible)
* [Ahmed Almasah's Udemy Course](https://www.udemy.com/course/red-hat-exams-rhce-ex294-ansible-automatiomation-ex407/)
* [Blog post at lisenet.com](https://www.lisenet.com/2019/ansible-sample-exam-for-ex294/)

## Infrastructure assumptions
In order to perform the exercises plan of the infrastructure must be established.
What I present is similar to configuration used by RedHat in their course preparing for the exam - RH294.
Look at [one of my repositories](https://github.com/mateuszstompor/rhce-environment) to save time provisioning the machines on your own and have a cluster that is you can exercise against


#### Hosts
There are five servers used in total throughout the objectives. 
All ansible code should be written and executed from the `controller` node.
Most of the exercises are targetted at changing configuration of managed host but modification of `controller` is something that the person preparing for the test should be able to do as well

* controller - control node
* managed1 - managed node
* managed2 - managed node
* managed3 - managed node
* managed4 - managed node

#### Network
Access to each host should be possible with use of short name as well as fqdn which is build by concatenating short name with `.example.com`, e. g. `controller.example.com`. All of the nodes should have NAT access on top of direct access to each other

#### Users
Initially, there is a single user created on the servers
* root - accessed by password `vagrant`

#### Authentication against other servers
Managed nodes can be accessed via ssh from the controller, without password with use of `root` user

#### System
All machines were provisioned with RHEL8/CentOS8 system

#### Requirements
* ansible 2.8 - on control node
* python3 - on both control and managed 
* sshd - up and running everywhere
