# TODOs

## sshd

- [ ] Make configuration idempotent (edit lines instead of copying file)
- [ ] Make sure key used by Ansible is there
- [ ] Do not restart if no changes were made

# Install basic packages

- [ ] Put package list in Ansible variable

# ufw

- [ ] Make sure we don't get locked out
- [ ] Make sure no reloads or restarts happen unless we make a change

# minidlna

- [ ] Do not restart if no changes were made

# docker

- [ ] Use non-deprecated way to trust Docker PPA
- [ ] [Check out Jeff Geerling's Ansible for Docker](https://github.com/geerlingguy/ansible-role-docker)
