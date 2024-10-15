# ansible_n100
Toy ansible playbook for home server. Not useful for anyone but here I have a place to pull from. Feel free to look but there's much better places to check out.

To use it, I typically run

```
ansible-playbook -Ki inventory.yml playbook.yml
```

-i is to indicate the inventory file and -K is to get prompted for the sudo password to elevate privileges.

My sources (not exhaustive, I have anyway not check out the sources fully):
 - Jeff Geerling's [Ansible for DevOps](https://www.ansiblefordevops.com/)
 - Jeff Geerling's [Youtube Channel](https://www.youtube.com/c/JeffGeerling)
 - [Wolfgang's channel](https://www.youtube.com/@WolfgangsChannel)
 - A nonending series of random webpages

# TODOs

## sshd

- [ ] Consider editing lines instead of copying file
- [ ] Make sure key used by Ansible is there
- [x] Do not restart if no changes were made

# Install basic packages

- [ ] Put package list in Ansible variable

# ufw

- [ ] Figure out how to deny incoming by default without getting locked out
- [x] Make sure no reloads or restarts happen unless we make a change

# minidlna

- [x] Do not restart if no changes were made

# docker

- [ ] Use non-deprecated way to trust Docker PPA
- [ ] [Check out Jeff Geerling's Ansible for Docker](https://github.com/geerlingguy/ansible-role-docker)
